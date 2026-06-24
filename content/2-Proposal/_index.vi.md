---
title: "Đề xuất dự án"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Money Manager – Hệ thống Quản lý Tài chính Cá nhân trên nền tảng AWS

## Giải pháp toàn diện cho quản lý tài chính cá nhân với AWS Cloud

### 1. Tóm tắt

Money Manager là một ứng dụng quản lý tài chính cá nhân chạy trên cả Web lẫn Mobile. Ứng dụng cho phép người dùng theo dõi thu chi, lập ngân sách, quản lý các hũ chi tiêu và mục tiêu tiết kiệm, dự báo tài chính, xuất báo cáo qua Excel/Email, scan hóa đơn bằng OCR, và đặc biệt có trợ lý AI tên Nova Money hỗ trợ tư vấn tài chính.

Về mặt kỹ thuật, hệ thống được xây dựng theo kiến trúc nhiều tầng — phía người dùng là ứng dụng Web/Mobile, phía server là các dịch vụ của AWS.

### 2. Vấn đề cần giải quyết

**Thực trạng**: Hiện tại, việc quản lý tài chính cá nhân thường được làm thủ công hoặc dùng các app đơn giản, thiếu khả năng phân tích sâu, dự báo xu hướng chi tiêu, và không có AI hỗ trợ đưa ra quyết định tài chính.

**Giải pháp**: Money Manager dùng kiến trúc AWS Cloud với High Availability, kết hợp AI (Google Gemini và OpenRouter GPT-OSS) để mang đến trải nghiệm quản lý tài chính đầy đủ — từ tracking thu chi, budgeting, dự báo tài chính, cho đến nhận diện hóa đơn qua OCR và chat với trợ lý AI Nova Money.

**Lợi ích**: Giúp người dùng tiết kiệm thời gian quản lý tài chính, chi tiêu thông minh hơn nhờ dự báo từ AI, đồng thời tạo nền tảng để phát triển thêm các tính năng Premium sau này.

### 3. Kiến trúc hệ thống

Toàn bộ hệ thống deploy trên AWS Cloud tại Region Singapore (ap-southeast-1), nằm trong một VPC trải trên 2 Availability Zone để đảm bảo High Availability.

#### Công nghệ sử dụng

- **Backend**: Spring Boot (Java 21), kiến trúc phân lớp Controller → Service → Repository
- **Frontend Web**: React 19 + Vite
- **Mobile**: React Native (Expo)
- **AI**: Google Gemini (chat, agent, OCR, dự báo) và OpenRouter GPT-OSS (phân tích báo cáo cho gói Premium)

#### Các dịch vụ AWS chính

- **Application Load Balancer (ALB)**: Đặt trong Public Subnet, phân phối request đến các EC2 phía sau, span 2 AZ.
- **Amazon EC2 + Auto Scaling Group**: Chạy backend Spring Boot trong Private Subnet, tự động scale theo tải.
- **EC2 Worker**: Instance riêng để xử lý background job (consume từ SQS).
- **Amazon Aurora MySQL + RDS Proxy**: Database chính, deploy multi-AZ. RDS Proxy giúp quản lý connection pool hiệu quả.
- **Amazon ElastiCache (Redis)**: Dùng cho cache, session và rate limit. Deploy HA trên 2 AZ.
- **Amazon DynamoDB**: Lưu lịch sử chat của Nova Money AI, truy xuất nhanh nhờ low latency.
- **Amazon SQS + DLQ**: Message queue cho các task nặng (export báo cáo Excel, render hóa đơn PDF, gửi báo cáo định kỳ). Có Dead-Letter Queue xử lý job lỗi.
- **AWS Lambda**: Chạy serverless để tạo file báo cáo và hóa đơn.
- **Amazon S3**: Lưu file báo cáo, hóa đơn PDF và ảnh invoice.
- **Amazon SNS**: Gửi email alert cho admin khi ngân sách vượt mức hoặc subscription sắp hết hạn.
- **Amazon CloudWatch**: Monitoring toàn bộ hệ thống — logs, metrics, alarms cho ALB, EC2, Aurora, Lambda, SQS.
- **NAT Gateway**: Cho phép EC2 trong Private Subnet gọi ra các service bên ngoài.
- **IAM Roles**: Phân quyền truy cập giữa các dịch vụ AWS.

#### Các luồng xử lý chính

- **Luồng người dùng**: User truy cập qua Web/Mobile → đi qua Cloudflare (DNS, WAF, chống DDoS, Rate Limit, Turnstile chống bot) → vào ALB → đến EC2 Web-API.
- **Luồng nghiệp vụ**: EC2 xử lý login (JWT + Google OAuth2), quản lý thu chi, ngân sách, hũ tiết kiệm → ghi vào Aurora MySQL (qua RDS Proxy), cache ở ElastiCache Redis.
- **Luồng AI chat**: User chat với Nova Money → lưu lịch sử vào DynamoDB → lấy context các tin nhắn gần nhất gửi kèm cho model AI.
- **Luồng async**: EC2 Web-API đẩy job vào SQS → EC2 Worker consume → gọi Lambda tạo file → lưu kết quả vào S3.
- **Luồng thông báo**: Khi có event cảnh báo → SNS gửi email cho Admin.
- **Luồng outbound**: EC2 → NAT Gateway → PayOS (thanh toán QR), Brevo SMTP (gửi email OTP, báo cáo), Google Gemini API.

### 4. Triển khai kỹ thuật

#### Các giai đoạn thực hiện

1. **Nghiên cứu và thiết kế**: Phân tích yêu cầu, vẽ kiến trúc AWS theo Well-Architected Framework, thiết kế database schema và API endpoints.
2. **Tính chi phí**: Dùng AWS Pricing Calculator ước tính cost cho Aurora, ElastiCache, EC2, Lambda, S3 và các service liên quan.
3. **Phát triển backend**: Code Spring Boot API (Java 21), tích hợp JWT/OAuth2, kết nối Aurora MySQL qua RDS Proxy, setup ElastiCache Redis.
4. **Phát triển frontend**: Xây giao diện Web bằng React 19 + Vite và app Mobile bằng React Native Expo.
5. **Tích hợp AI**: Connect Google Gemini cho chat/agent/OCR/dự báo, OpenRouter GPT-OSS cho phân tích report Premium.
6. **Deploy và testing**: Triển khai lên AWS (VPC, EC2 ASG, ALB, Aurora, ElastiCache), cấu hình Cloudflare, chạy test end-to-end.

#### Yêu cầu kỹ thuật

- **Backend**: Java 21, Spring Boot, Spring Security (JWT + OAuth2), Spring Data JPA, Hibernate.
- **Frontend**: React 19, Vite, React Native (Expo), responsive design.
- **Database**: Aurora MySQL (multi-AZ), DynamoDB (chat history), ElastiCache Redis (cache/session).
- **Infrastructure**: VPC (2 AZ), ALB, EC2 ASG (Graviton), NAT Gateway, RDS Proxy, SQS + DLQ, Lambda, S3, SNS, CloudWatch, IAM Roles.
- **Security**: Cloudflare (WAF, DDoS protection, Rate Limit, Turnstile), HTTPS, IAM policies, Security Groups.

### 5. Lộ trình triển khai

- **Tuần 1–6 (20/04 – 29/05)**: Học các dịch vụ AWS nền tảng (IAM, VPC, EC2, RDS, S3, Lambda, API Gateway, CloudFormation, DynamoDB) qua lab trên CloudJourney.
- **Tuần 7–8 (01/06 – 12/06)**:
    - Tìm hiểu source code, phân tích kiến trúc, setup môi trường dev.
    - Deploy thử lên EC2, cấu hình RDS, tích hợp S3/CloudFront.
    - Nghiên cứu Well-Architected Framework, AWS SAM và lên kiến trúc cho dự án.
- **Tuần 9 (15/06 – 19/06)**:
    - Phát triển các chức năng chính: backend Spring Boot, frontend React, kết nối database.
    - Deploy lên EC2 trong Private Subnet, cấu hình ALB và Auto Scaling Group.
- **Tuần 10 (22/06 – 26/06)**:
    - Setup IAM, bảo mật (JWT, OAuth2, Cloudflare WAF).
    - Deploy backend Spring Boot lên EC2 ASG, cấu hình ALB, Aurora MySQL, ElastiCache.
    - Chạy unit test, integration test, load test và tối ưu performance.
- **Tuần 11 (29/06 – 03/07)**:
    - Tối ưu UI/UX cho Web (React 19 + Vite) và Mobile (React Native Expo), chạy E2E test.
    - Cấu hình CloudWatch monitoring, chuẩn bị slide và demo.
    - Code review, viết báo cáo kiến trúc, backup dữ liệu.
- **Tuần 12 (06/07 – 10/07)**:
    - Hỗ trợ sau deploy, hardening bảo mật, tối ưu chi phí AWS.
    - Test recovery/failover (Aurora multi-AZ, ElastiCache HA).
    - Nộp báo cáo và thuyết trình.

### 6. Ước tính chi phí

**Chi phí hạ tầng hàng tháng (ước tính)**:

| Dịch vụ | Chi phí |
|---|---|
| Amazon EC2 (ASG – Graviton) | ~15,00 USD/tháng (t4g.small, tối thiểu 2 instance) |
| Application Load Balancer | ~16,20 USD/tháng |
| Amazon Aurora MySQL | ~29,00 USD/tháng (db.t4g.medium, multi-AZ) |
| Amazon ElastiCache (Redis) | ~12,00 USD/tháng (cache.t4g.micro, 2 node HA) |
| Amazon DynamoDB | ~1,00 USD/tháng (on-demand, lưu chat history) |
| Amazon S3 | ~0,50 USD/tháng (lưu báo cáo, hóa đơn, ảnh) |
| AWS Lambda | ~0,00 USD/tháng (free tier) |
| Amazon SQS | ~0,00 USD/tháng (free tier) |
| Amazon SNS | ~0,00 USD/tháng (free tier) |
| NAT Gateway | ~32,00 USD/tháng (outbound traffic) |
| Amazon CloudWatch | ~3,00 USD/tháng (logs, metrics, alarms) |
| Cloudflare (Free plan) | 0,00 USD/tháng |
| **Tổng** | **~108,70 USD/tháng (~1.304,40 USD/năm)** |

### 7. Đánh giá rủi ro

| Rủi ro | Mức độ | Xử lý |
|---|---|---|
| Lỗi kết nối database | Ảnh hưởng cao, xác suất thấp | RDS Proxy quản lý connection pool |
| Quá tải hệ thống | Ảnh hưởng cao, xác suất trung bình | Auto Scaling Group tự co giãn |
| Mất dữ liệu | Ảnh hưởng cao, xác suất thấp | Aurora multi-AZ với automated backup |
| Tấn công DDoS/Bot | Ảnh hưởng trung bình, xác suất trung bình | Cloudflare WAF + Rate Limit + Turnstile |
| Vượt budget AWS | Ảnh hưởng trung bình, xác suất trung bình | CloudWatch billing alarm |

#### Phương án dự phòng

- Auto failover giữa 2 AZ cho Aurora MySQL và ElastiCache Redis.
- Dead-Letter Queue cho SQS để retry hoặc debug các job bị lỗi.
- CloudWatch Alarm tự động báo khi có vấn đề về performance hoặc error rate tăng.

### 8. Kết quả mong đợi

**Về kỹ thuật**: Xây dựng được hệ thống quản lý tài chính cá nhân chạy ổn định trên AWS với High Availability, hỗ trợ cả Web và Mobile. Tích hợp AI (Google Gemini, OpenRouter) cho dự báo tài chính, OCR hóa đơn và trợ lý Nova Money. Xử lý async hiệu quả với SQS + Lambda cho việc export báo cáo và render hóa đơn.

**Về lâu dài**: Hệ thống có thể scale linh hoạt nhờ Auto Scaling Group và kiến trúc multi-AZ. Có tiềm năng phát triển thêm tính năng Premium (phân tích chuyên sâu qua OpenRouter GPT-OSS), tích hợp thêm payment gateway và mở rộng ra thị trường quốc tế.
