---
title: "Event 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---


# Summary Report: Event 1

### Event Objectives

- How to make learning as addictive as social media.
- How to communicate and use AI efficiently with minimal resources while still achieving positive results.
- Shift the mindset of young people in the AI era and equip them with essential soft skills.
- Guide on using AI Agents to play the role of a real team.

### Speakers

- **Mr. Long** - Admin of FCAJ
- **Mr. Thịnh** - DevOps/Cloud Engineer at FCAJ
- **Mr. Khang** - Solution Architect at Cloud Kinetic
- **Ms. Thảo** - Software Developer at VIB International Bank

### Key Highlights

#### "Brain Hack" to Make Learning as Addictive as Social Media

- **Procrastination reality**: Learners tend to prioritize games or social media (TikTok, Facebook) because they provide immediate rewards and stimulate the brain's curiosity, whereas learning typically yields delayed results.
- **Dopamine mechanism**: Dopamine is not released when receiving a reward but when the brain anticipates an upcoming reward. The event taught how to turn learning into a "Dopamine gamble" using a random reward system after every 10-15 minutes of focus.
- **Applied behavioral psychology**:
- **Loss Aversion**: Leverage the fear of breaking a streak (like Duolingo streaks, TikTok streaks) to maintain a daily learning check-in schedule.
- **2-Minute Rule & Chunking**: Trick the amygdala by breaking down huge knowledge blocks into ultra-small tasks (read 1 page of a book, create 1 Cloud account) to accumulate a sense of daily achievement.

#### Advanced Prompt Engineering for LLMs

- **7 core prompt components**: To optimize AI response quality and avoid generic output, a standard prompt needs a tight structure including: Role, Instruction, Context, Input, Output Format, Example, and Constraint.
- **Token & Cost Optimization**: Understanding how AI models split text into tokens (sub-word). Note that Vietnamese consumes roughly double the tokens of English, increasing API operational costs.
- **AI reasoning techniques**: Introduction and comparison of methods that help AI models think more logically when solving complex problems, such as Chain-of-Thought, Self-Consistency, and Tree-of-Thought.

#### Long-Term Investment Strategy & Work Mindset in the AI Era

**Mindset for Facing AI Development**

- **AI is merely an amplifier**: Analysis of real hiring scenarios where most submitted assignments show AI intervention, but most candidates don't truly understand the code's essence. Bad AI will make you worse, but with good thinking, AI will multiply your productivity.
- **Don't "Outsource" understanding**: You can use AI to brainstorm or develop ideas, but core understanding and thinking can never be outsourced. Employers always prefer someone scoring 6-7 who grasps system thinking over someone scoring 8-9 through AI copying.
- **The importance of "Why"**: Shift focus from only caring about what to do (What) to complete assignments toward questioning why (Why) a solution is chosen. The corporate environment has no absolute right/wrong, only contextual fit.

**Core Professional Qualities**

- **Integrity at work**: An engineer with integrity proactively decomposes original requirements to explore and handle dozens of edge cases, instead of doing the bare minimum to meet surface-level requirements. This long-term value builds trust among team members in an organization.
- **Embrace mistakes**: Willingness to face and accumulate lessons from errors. Companies always set aside a risk budget for freshers' mistakes in exchange for their onboarding and growth.

**Long-Term Benefits Strategy**

- From a fresher's and final-year student's perspective, avoid short-term thinking or quantifying work value solely based on Salary.
- Set proper expectations and balance your benefit system on 4 long-term pillars: **Experience**, **Network**, **Knowledge**, and **Growth**.

**Teamwork Spirit**

- **Don't go alone**: A large real-world project is very difficult to run solo. Proactively forming a team not only improves technical skills but also demonstrates collaboration ability, management skills, and mutual support to employers.

#### AI-Powered Software Development Process Using the BMX Method

**The "Junk Code" Problem from AI Overuse**

- Analysis of the common mistake where programmers just keep feeding prompts into a regular chat window and leave the entire project to AI.
- Stuffing too many unstructured requests overwhelms the AI's Context Window, gradually forgetting earlier contexts. The result is a mess of "junk code" full of bugs, hard to fix, and impossible to deploy.

**Document-Driven Philosophy of the BMX Method**

- Introduction of the open-source BMX method (Through Method for Agile Development) that completely changes how we code with AI.
- Shift focus from managing through code to strictly managing through a well-structured documentation system (VOD/Architect file). Core philosophy: "It's not about what the code looks like, but how well you write the documentation for it." When documentation is solid, AI automatically generates accurate, low-bug code.

**Role Decomposition of AI Agents as a Real Team**

- BMX defines and breaks a large project into small Epics/User Stories, tightly controlling task status (Draft, Approved, Review, Blocked), and assigns tasks to specialized AI Agents:

- **PM Agent & Architect Agent**: Responsible for analyzing initial requirements, brainstorming directly with humans, and designing system architecture through technical documentation.
- **PO & Scrum Master Agent**: Break down large documents into smaller tasks for easier Context Window management, preventing AI from being overwhelmed. Humans act as approvers before allowing AI to write code.
- **Developer Agent**: Automatically extract approved stories into sub-tasks to write precise code for each isolated feature.
- **Review Agent (QA/QC)**: Execute continuous automated testing and bug detection loops until the software bug rate reaches zero.

**Core Advantage: Eliminating AI Hallucination**

- Through strict process separation, each feature is handled by its dedicated Agent without overlapping knowledge onto other features.
- Minimizes the Context Window, thereby controlling and reducing AI Hallucination, making the system easy to maintain, modify, or upgrade as the project scales.

### Key Takeaways

#### Personal Development & Design Mindset

- **Designing a smart learning environment**: Understanding that the winner in self-learning is not the most diligent person, but the one who builds a space and system that stimulates the brain to release Dopamine consistently.
- **Why-first approach**: Always start with the "Why" question when choosing any technology or solution, instead of only caring about how to finish the assignment (What). The corporate environment has no absolute right/wrong, only the most suitable solution for the context.
- **Understanding cannot be "Outsourced"**: Recognizing that AI is merely an amplifier. Humans can use AI to develop ideas, but core system understanding must belong to oneself.
- **Document-Driven philosophy**: Shift mindset from managing projects through code to managing strictly through documentation (VOD/Architect file). Only when documentation is solid can AI generate accurate code.

#### Technical Architecture & Cloud Technology

- **7-component Prompt structure**: A practical method to optimize LLM response quality, including: Role, Instruction, Context, Input, Output Format, Example, and Constraint.
- **Token optimization strategy**: Understanding API cost calculation based on tokens and the language-specific characteristic of Vietnamese (consuming roughly double the tokens of English).
- **AI reasoning techniques**: Mastering advanced patterns that help AI think logically, such as Chain-of-Thought, Self-Consistency, and Tree-of-Thought.
- **AWS Compute spectrum**: Criteria for selecting compute services from traditional virtualization to Cloud Native and Serverless: Amazon EC2 → Amazon ECS → AWS Fargate → AWS Lambda.
- **System decomposition via AI Agents**: Method for splitting a large project into isolated Epics/User Stories and assigning them to specialized Agents (PM, Architect, Developer, Review Agents) to control the Context Window and eliminate AI Hallucination.

#### Long-Term Development Strategy & Self-Positioning

- **Balanced benefits system**: For a fresher, don't focus short-sightedly on immediate salary; instead, quantify work value based on 4 long-term pillars: Experience, Network, Knowledge, and Growth.
- **Integrity culture**: Awareness of proactively exploring and handling all system edge cases even when no one is watching or managing.
- **Embrace mistakes**: View mistakes as a necessary part of accumulating real experience. Understand that companies always set aside a risk budget for freshers' mistakes in exchange for their growth.

### Applying to Work

- **Apply the Dopamine mechanism to self-learning**: Set up a random reward system after every 10-15 minutes of focus and use Loss Aversion technique (streak fear) to maintain daily tech learning discipline.
- **Apply the 2-Minute Rule & Chunking**: Break down huge knowledge blocks (like AWS certifications) into ultra-small tasks (read 1 doc page, create 1 account, test 1 service) to tackle immediately.
- **Optimize workflow with AI**: Implement the 7-component prompt structure into daily workflow to improve AI code output quality.
- **Try the BMX method**: Apply the Document-driven management model and break tasks into Epics/Stories before feeding them into AI tools to avoid knowledge overlap and reduce messy bugs.
- **Serverless adoption**: Experiment with integrating Serverless (AWS Lambda) and storage/auth solutions (S3, DynamoDB, Cognito) for personal projects or major assignments.
- **Form a team**: Proactively find teammates to work on side projects together, enhancing collaboration skills, teamwork, and long-term mutual development.

### Event Experience

Attending **"FCAJ Community Day"** was an incredibly rewarding experience, giving me a comprehensive view not only of technical aspects (Cloud, Generative AI) but also of real-world career thinking in the new era. Key experiences included:

#### Learning from highly skilled speakers
- Speakers from AWS Study Group, VIB Bank, and experienced Solutions Architects shared very practical stories and best practices from the perspective of those who came before.
- Through case studies and live project demos (Prompt Optimizer, BMX Method), I gained a clearer understanding of how businesses operate and use AI tools to 10x productivity instead of being replaced by AI.

#### Hands-on technical experience
- Directly followed a live demo of a Cloud Native solution architecture on AWS combined with Amazon Bedrock for prompt optimization.
- Learned how to decompose a large software system into small User Stories through specialized AI Agents to strictly control AI Hallucination.
- Understood the trade-offs in cost and tokens when building AI applications using Vietnamese compared to English.

#### Career orientation and mindset shift
- Received profound advice on interview roadmaps, internship hiring, and how companies evaluate assignments.
- The workshop helped me realize the importance of **Integrity** when building products, the courage to **Embrace mistakes**, and a long-term vision of benefits when entering the IT industry.

#### Networking and discussions
- The event provided opportunities to network and connect on LinkedIn directly with industry experts and like-minded peers.
- The open space of the Meetup helped relieve the anxiety and pressure of being a "final-year student who hasn't started working yet" and gave me more motivation to design my own development environment.

#### Some event photos
<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 10px;">
    {{< rimg src="/images/4-EventParticipated/4.1-Event1/anhevent1.jpg" alt="Event photo 1" style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px;" >}}
    {{< rimg src="/images/4-EventParticipated/4.1-Event1/anhevent2.jpg" alt="Event photo 2" style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px;" >}}
</div>
