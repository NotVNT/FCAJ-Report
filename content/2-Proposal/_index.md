---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Money Manager – Personal Finance Management System on AWS

## A Comprehensive Solution for Personal Finance Management with AWS Cloud

### 1. Overview

Money Manager is a personal finance management application running on both Web and Mobile. The application allows users to track income and expenses, create budgets, manage spending jars and savings goals, forecast finances, export reports via Excel/Email, scan invoices using OCR, and features an AI assistant named Nova Money for financial advice.

On the technical side, the system is built with a multi-tier architecture — the user-facing side is a Web/Mobile application, and the server side consists of AWS services.

### 2. Problem Statement

**Current situation**: Personal finance management is typically done manually or using simple apps that lack deep analytical capabilities, spending trend forecasting, and AI-powered financial decision support.

**Solution**: Money Manager uses an AWS Cloud architecture with High Availability, combined with AI (Google Gemini and OpenRouter GPT-OSS) to deliver a complete finance management experience — from income/expense tracking, budgeting, financial forecasting, to invoice recognition via OCR and chatting with the Nova Money AI assistant.

**Benefits**: Helps users save time on financial management, spend smarter with AI-powered forecasts, while creating a foundation for future Premium feature development.

### 3. System Architecture

The entire system is deployed on AWS Cloud in the Singapore region (ap-southeast-1), within a VPC spanning 2 Availability Zones to ensure High Availability.

#### Technologies Used

- **Backend**: Spring Boot (Java 21), layered architecture Controller → Service → Repository
- **Frontend Web**: React 19 + Vite
- **Mobile**: React Native (Expo)
- **AI**: Google Gemini (chat, agent, OCR, forecasting) and OpenRouter GPT-OSS (report analysis for Premium plan)

#### Key AWS Services

- **Application Load Balancer (ALB)**: Placed in Public Subnet, distributes requests to backend EC2 instances, spans 2 AZs.
- **Amazon EC2 + Auto Scaling Group**: Runs Spring Boot backend in Private Subnet, automatically scales based on load.
- **EC2 Worker**: Dedicated instance for processing background jobs (consuming from SQS).
- **Amazon Aurora MySQL + RDS Proxy**: Primary database, deployed multi-AZ. RDS Proxy manages connection pooling efficiently.
- **Amazon ElastiCache (Redis)**: Used for caching, sessions, and rate limiting. Deployed HA across 2 AZs.
- **Amazon DynamoDB**: Stores Nova Money AI chat history for low-latency access.
- **Amazon SQS + DLQ**: Message queue for heavy tasks (Excel report export, PDF invoice rendering, periodic report sending). Includes Dead-Letter Queue for failed job handling.
- **AWS Lambda**: Serverless execution for generating report files and invoices.
- **Amazon S3**: Stores report files, PDF invoices, and invoice images.
- **Amazon SNS**: Sends email alerts to admins when budgets are exceeded or subscriptions are about to expire.
- **Amazon CloudWatch**: Full system monitoring — logs, metrics, alarms for ALB, EC2, Aurora, Lambda, SQS.
- **NAT Gateway**: Enables EC2 instances in Private Subnet to call external services.
- **IAM Roles**: Manages access permissions between AWS services.

#### Main Processing Flows

- **User flow**: User accesses via Web/Mobile → passes through Cloudflare (DNS, WAF, DDoS protection, Rate Limit, Turnstile anti-bot) → reaches ALB → forwarded to EC2 Web-API.
- **Business flow**: EC2 handles login (JWT + Google OAuth2), manages income/expenses, budgets, savings jars → writes to Aurora MySQL (via RDS Proxy), caches in ElastiCache Redis.
- **AI chat flow**: User chats with Nova Money → history saved to DynamoDB → recent message context retrieved and sent with the AI model.
- **Async flow**: EC2 Web-API pushes jobs to SQS → EC2 Worker consumes → invokes Lambda to generate files → saves results to S3.
- **Notification flow**: When alert events occur → SNS sends email to Admin.
- **Outbound flow**: EC2 → NAT Gateway → PayOS (QR payment), Brevo SMTP (send OTP emails, reports), Google Gemini API.

### 4. Technical Implementation

#### Implementation Phases

1. **Research and design**: Analyze requirements, design AWS architecture following Well-Architected Framework, design database schema and API endpoints.
2. **Cost estimation**: Use AWS Pricing Calculator to estimate costs for Aurora, ElastiCache, EC2, Lambda, S3, and related services.
3. **Backend development**: Code Spring Boot API (Java 21), integrate JWT/OAuth2, connect to Aurora MySQL via RDS Proxy, setup ElastiCache Redis.
4. **Frontend development**: Build Web UI with React 19 + Vite and Mobile app with React Native Expo.
5. **AI integration**: Connect Google Gemini for chat/agent/OCR/forecasting, OpenRouter GPT-OSS for Premium report analysis.
6. **Deploy and testing**: Deploy to AWS (VPC, EC2 ASG, ALB, Aurora, ElastiCache), configure Cloudflare, run end-to-end tests.

#### Technical Requirements

- **Backend**: Java 21, Spring Boot, Spring Security (JWT + OAuth2), Spring Data JPA, Hibernate.
- **Frontend**: React 19, Vite, React Native (Expo), responsive design.
- **Database**: Aurora MySQL (multi-AZ), DynamoDB (chat history), ElastiCache Redis (cache/session).
- **Infrastructure**: VPC (2 AZ), ALB, EC2 ASG (Graviton), NAT Gateway, RDS Proxy, SQS + DLQ, Lambda, S3, SNS, CloudWatch, IAM Roles.
- **Security**: Cloudflare (WAF, DDoS protection, Rate Limit, Turnstile), HTTPS, IAM policies, Security Groups.

### 5. Implementation Timeline

- **Week 1–6 (Apr 20 – May 29)**: Learn foundational AWS services (IAM, VPC, EC2, RDS, S3, Lambda, API Gateway, CloudFormation, DynamoDB) through CloudJourney labs.
- **Week 7–8 (Jun 01 – Jun 12)**:
    - Study source code, analyze architecture, set up dev environment.
    - Trial deploy on EC2, configure RDS, integrate S3/CloudFront.
    - Research Well-Architected Framework, AWS SAM, and design project architecture.
- **Week 9 (Jun 15 – Jun 19)**:
    - Develop core features: Spring Boot backend, React frontend, database connection.
    - Deploy to EC2 in Private Subnet, configure ALB and Auto Scaling Group.
- **Week 10 (Jun 22 – Jun 26)**:
    - Setup IAM, security (JWT, OAuth2, Cloudflare WAF).
    - Deploy Spring Boot backend to EC2 ASG, configure ALB, Aurora MySQL, ElastiCache.
    - Run unit tests, integration tests, load tests, and performance optimization.
- **Week 11 (Jun 29 – Jul 03)**:
    - Optimize UI/UX for Web (React 19 + Vite) and Mobile (React Native Expo), run E2E tests.
    - Configure CloudWatch monitoring, prepare slides and demo.
    - Code review, write architecture report, backup data.
- **Week 12 (Jul 06 – Jul 10)**:
    - Post-deploy support, security hardening, AWS cost optimization.
    - Test recovery/failover (Aurora multi-AZ, ElastiCache HA).
    - Submit report and presentation.

### 6. Cost Estimation

**Monthly infrastructure cost (estimated)**:

| Service | Cost |
|---|---|
| Amazon EC2 (ASG – Graviton) | ~$15.00/month (t4g.small, minimum 2 instances) |
| Application Load Balancer | ~$16.20/month |
| Amazon Aurora MySQL | ~$29.00/month (db.t4g.medium, multi-AZ) |
| Amazon ElastiCache (Redis) | ~$12.00/month (cache.t4g.micro, 2 node HA) |
| Amazon DynamoDB | ~$1.00/month (on-demand, chat history storage) |
| Amazon S3 | ~$0.50/month (reports, invoices, images) |
| AWS Lambda | ~$0.00/month (free tier) |
| Amazon SQS | ~$0.00/month (free tier) |
| Amazon SNS | ~$0.00/month (free tier) |
| NAT Gateway | ~$32.00/month (outbound traffic) |
| Amazon CloudWatch | ~$3.00/month (logs, metrics, alarms) |
| Cloudflare (Free plan) | $0.00/month |
| **Total** | **~$108.70/month (~$1,304.40/year)** |

### 7. Risk Assessment

| Risk | Severity | Mitigation |
|---|---|---|
| Database connection failure | High impact, low probability | RDS Proxy manages connection pool |
| System overload | High impact, medium probability | Auto Scaling Group auto-scales |
| Data loss | High impact, low probability | Aurora multi-AZ with automated backup |
| DDoS/Bot attack | Medium impact, medium probability | Cloudflare WAF + Rate Limit + Turnstile |
| AWS budget overrun | Medium impact, medium probability | CloudWatch billing alarm |

#### Contingency Plan

- Auto failover between 2 AZs for Aurora MySQL and ElastiCache Redis.
- Dead-Letter Queue for SQS to retry or debug failed jobs.
- CloudWatch Alarm automatically notifies when performance issues or error rates increase.

### 8. Expected Outcomes

**Technical**: Build a stable personal finance management system on AWS with High Availability, supporting both Web and Mobile. Integrate AI (Google Gemini, OpenRouter) for financial forecasting, invoice OCR, and the Nova Money assistant. Efficient async processing with SQS + Lambda for report export and invoice rendering.

**Long-term**: The system can scale flexibly thanks to Auto Scaling Group and multi-AZ architecture. Potential for further Premium feature development (deep analysis via OpenRouter GPT-OSS), additional payment gateway integration, and expansion into international markets.
