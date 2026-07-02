---
title: "Event 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---



# Summary Report: Event 2

### Event Objectives

- Develop a mindset for building real-world products.
- Share hands-on experience from Hackathon competitions.
- Raise awareness of information security and compliance.
- Optimize infrastructure and Cloud system operational costs.
- Promote confident communication and critical thinking.
- Understand the essence of technology to design sustainable systems.

### Speakers

- **Mr. Tinh Trương** - Platform Engineer at GoTymex
- **Mr. Phạm Nguyễn Hải Anh** - G-AsiaPacific Vietnam, AWS Community Builder
- **Mr. Thịnh** - DevOps/Cloud Engineer at FCAJ
- **UTMorpho** - LotusHacks 2026 Team
- **Mr. Duc Dao** - Solution Architect at Kinetics
- **Ms. Cát Vy** - Senior Business Systems Analyst at VPBank

### Key Highlights

#### Labor Market Trends & New Requirements for IT Professionals

- **The transition period reality**: The global AI infrastructure investment race among tech giants creates short-term cost optimization pressure, making the job market (especially Intern/Fresher positions) more competitive than ever (actual competition ratio at enterprises can reach 1:50).
- **New wave of jobs**: The AI boom reduces software creation costs, leading to a surge in demand for system maintenance, operations, and expansion. New roles such as Platform Engineering and Off-Platform Engineering emerge to handle enterprise systems.
- **3 mandatory weapons to equip**:
    - **Solid technical foundation**: A university degree remains a必要条件 (CV filter) for large organizations.
    - **Real-world domain knowledge (Domain/Case study)**: Must understand the operating model of the target industry (e.g., Finance - Banking).
    - **Real product (Product Mindset)**: Instead of just demo assignments, candidates must own real-world products to convince employers.

#### Mastering Context in AI Communication

- **The "Internet Buller" problem**: The habit of collecting every prompt, plugin, and template rule from the internet and using them all in one chat session dilutes AI context, causing constant context switching that leads to confusion and buggy code.
- **Building the right and sufficient Context**: When prompting AI, clearly provide: Goal, Role/Persona level, Desired Format, and especially only include project/enterprise-specific documents/rules (general knowledge AI already has).
- **The nature of Temperature = 0**: When lowering temperature to 0, the LLM switches to Greedy Decoding (Argmax) — always picking the highest probability token. However, due to GPU decimal rounding techniques and prompt batching for cost optimization by API providers (Inference Optimization), results between runs can still vary (Randomness).
- **Mitigation Strategy**: For stable Production systems, wrap downstream services to handle format errors, consider self-hosting models locally for full control, or use parallel multi-Agent mechanisms to vote for the most consensual result.

#### Real-World AI Product Development Experience (Hackathon Case Study)

- **"UTMorpho" Project (Hackathon Winner)**: A real-world demonstration of building an AI Editor application that generates UI and allows drag-and-drop editing directly on that UI from sketches or images within 36 hours.
- **Collaborative Multi-Agent Architecture**: The project uses a layered structure of 3 specialized Agents:
    - **Agent 1 (Vision Agent)**: Reads and analyzes input images into JSON files.
    - **Agent 2 (Layout Agent)**: Receives JSON to calculate dimensions, layout, and CSS.
    - **Agent 3 (Design Agent)**: Generates complete HTML/CSS code.
- **Hard-learned lessons from reality**:
    - Avoid the overthinking/overfeature trap: Cut unnecessary features, focus only on optimizing the Core Feature to meet deadlines.
    - Solve your own problem: The best ideas don't need to be grandiose — find ideas that solve your development team's daily pain points.

#### AI Agent Technology & Data Analytics Applications

- **Evolution from Chatbot to Agent**: Unlike traditional Chatbots that only reply with text, an AI Agent is an LLM brain equipped with "extended arms" — Actions/Functions (via protocols like MCP) to directly act: schedule meetings, create dashboards, send emails...
- **Amazon Q Business / QuickSight Application (Demo)**: Business users (Manager, CEO) without technical skills simply upload raw Excel data files into the chat, and the AI Agent automatically analyzes and builds visual dashboards in Vietnamese.
- **Meeting automation**: Agents can automatically transcribe meeting audio, summarize decisions, and automatically distribute Next Steps to each member's email via Microsoft Teams or Outlook.

#### New Pricing Model & CloudFront CDN Security Foundation

- **Flat-rate Pricing**: AWS launches fixed CDN plans (Free, Pro, Business, Premium) instead of traditional Pay-as-you-go. This completely solves the "Bill Spike" fear when systems face DDoS attacks or abnormal traffic spikes. Exceeding the limit only throttles bandwidth without extra charges.
- **Ultra-fast internal network (AWS Backbone)**: With nearly 700 PoPs directly connected to major ISPs, traffic from CDN to the Origin server travels through AWS's internal fiber optics, bypassing the public internet and preventing congestion when undersea cables are cut.
- **Advanced security at the Edge**:
    - Stop volumetric DDoS attacks at the Edge server in the Botnet's home country, preventing malicious traffic from reaching the origin server.
    - Apply S2N encryption library to resist quantum computer decryption and Mutual TLS (mTLS) requiring certificate authentication from both sides (Client & Server), strongly applicable to the Finance industry.
- **VPC Origin feature**: Create a hidden tunnel completely concealing the Origin server in a Private Subnet from the Internet, only allowing CloudFront direct access.

#### Enterprise-Grade Multi-Agent Architecture

- **Real-world problem**: Designing a Multi-Agent system to evaluate credit scores for Vietnamese Startup enterprises — entities typically rejected by traditional banking models due to lack of 3-year financial reports or collateral assets.
- **Enterprise specialization breakdown**: The system is designed as a Credit Committee consisting of a Host (Orchestrator) coordinating specialized Sub-Agents: **Financial Analyst** (cash flow processing), **Market Analyst** (scanning TAM/SAM/SOM market share), **Team Evaluator** (scanning founder reputation on LinkedIn/Facebook), and **Risk Assessor** (risk evaluation).
- **Security & Compliance barriers**: In large enterprises, security always comes before technology. AI tools cannot be arbitrarily plugged in due to data leakage risks (MCP attack vector). Every AI-generated result process must have Human-in-the-loop review and Audit trails, because before the law, humans bear ultimate responsibility — not AI.

#### Some event photos
<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 10px;">
    {{< rimg src="/images/4-EventParticipated/4.2-Event2/event1.jpg" alt="Event photo 1" style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px;" >}}
    {{< rimg src="/images/4-EventParticipated/4.2-Event2/event2.jpg" alt="Event photo 2" style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px;" >}}
    {{< rimg src="/images/4-EventParticipated/4.2-Event2/event3.jpg" alt="Event photo 3" style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px;" >}}
    {{< rimg src="/images/4-EventParticipated/4.2-Event2/event4.jpg" alt="Event photo 4" style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px;" >}}
    {{< rimg src="/images/4-EventParticipated/4.2-Event2/event5.jpg" alt="Event photo 5" style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px;" >}}
    {{< rimg src="/images/4-EventParticipated/4.2-Event2/event6.jpg" alt="Event photo 6" style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px;" >}}
</div>
