---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---


# Building Reliable Multi-Step Workflows with AWS Lambda Durable Functions

### What Are Durable Functions?

Durable Functions are regular Lambda functions with "durable execution" enabled. This feature extends Lambda's programming model with two new primitives — **"steps"** and **"waits"** — enabling automatic checkpointing, recovery after failures, and pausing execution for up to a year with no compute charges during idle periods. You don't need to manage additional infrastructure or write custom state management and error handling code.

The underlying technical mechanism is **checkpoint and replay**: when a failure occurs, Lambda re-runs the function from the beginning but skips already completed steps (which have checkpoints) and reuses saved results, ensuring no progress is lost.

### Problems with Traditional Lambda

With standard Lambda, your code runs from start to finish in a single invocation and is completely stateless. This creates three major limitations when building complex workflows:

- **State loss on failure**: If an error occurs at any step, the entire function must be retried from scratch; all state must be manually saved to DynamoDB or S3.
- **Time limit**: A single execution is capped at 15 minutes, unsuitable for long-running processes or those requiring human approval.
- **Manual idempotency handling**: Developers must protect against duplicate invocations and build safe deployment strategies themselves.

### How It Works: Checkpoint & Replay

Durable Functions solves these problems with two core primitives in the open-source Durable Execution SDK:

- **Step – `context.step()`**: Wraps a block of business logic for automatic checkpointing and retry. Once a step completes, it is skipped in subsequent replays.
- **Wait – `context.wait()` / callback**: Pauses execution for a period of time or until an external signal is received (e.g., human approval). During the wait, the function is suspended with no compute charges, then automatically resumes.

The architecture diagram below illustrates an AI workflow using Durable Functions: the client calls via API Gateway to a Lambda function (with durable execution enabled); the function uses `step()` to call Bedrock (LLM) and saves results to DynamoDB — each step is automatically checkpointed; uses `wait()`/callback to pause for human approval then resume; execution state is emitted to EventBridge and CloudWatch for monitoring.

### Key Highlights & Core Benefits

- **Automatic fault tolerance**: The SDK handles checkpointing, retries with configurable backoff, and ensures idempotency (only one execution per request even if upstream retries).
- **Pause up to one year**: Ideal for human-in-the-loop workflows, approval processes, or scheduled processing — no compute charges during idle periods.
- **Same Lambda experience**: Still a Lambda function with the same event handler and integrations; simply toggle "durable execution" when creating the function.
- **Multi-language support**: SDK supports JavaScript, TypeScript, Python, and Java (Java in Developer Preview, compatible with Java 17+).

### Ideal Use Cases

- **Multi-step AI workflows**: Orchestrate chains of LLM calls, tool invocations, and result processing safely even when a call fails.
- **Order & payment processing**: Maintain transaction state across failures with automatic retries; orchestrate authorization, fraud checks, and settlements across multiple providers.
- **Human-in-the-loop approvals**: Document review, leave request approval — pause for human decisions before proceeding.
- **Scheduled / long-running tasks**: Multi-day onboarding, subscription trials, delayed notifications, time-windowed batch processing.

### Source Code Example (Python)

After enabling durable execution and adding the SDK, use `DurableContext` to wrap each business step. The core concepts are `context.step()` and `context.wait()`:

```
def handler(event, context):
    # Step 1: call LLM - automatically checkpointed
    summary = context.step("summarize", lambda: call_llm(event))

    # Step 2: wait for human approval (free compute while waiting)
    decision = context.wait_for_callback("approval")

    # Step 3: only runs when approved - skips completed steps on replay
    if decision == "approved":
        context.step("persist", lambda: save_result(summary))
```

Note: although the total workflow can last up to a year, each Lambda container still runs for a maximum of 15 minutes between checkpoint/wait points.

### Release Status

Lambda Durable Functions was announced on **December 2, 2025** (re:Invent 2025), initially GA in US East (Ohio) with Python (3.13, 3.14) and Node.js (22, 24) runtimes, then expanded to more regions. Can be enabled via Console, AWS CLI, SAM, CloudFormation, CDK, or SDK. The Java SDK launched in Developer Preview on February 26, 2026.

<div style="display: flex; gap: 20px; flex-wrap: wrap;">
    <img src="/images/3-BlogsPosted/3.3-Blog3/blog3_img.jpg" alt="Blog 3 image" width="400" style="border-radius: 8px;">
</div>

### Conclusion

AWS Lambda Durable Functions blurs the line between Lambda's simplicity and the complexity of workflow orchestration systems. Instead of piecing together Step Functions, SQS, and DynamoDB, you write sequential logic in a single function and let the SDK handle checkpointing, retries, and pauses. This is an ideal choice for multi-step AI workflows, order processing, and human-in-the-loop approval processes.

### References

- [Build multi-step applications and AI workflows with AWS Lambda Durable Functions](https://aws.amazon.com/vi/blogs/aws/build-multi-step-applications-and-ai-workflows-with-aws-lambda-durable-functions/)
- [Building fault-tolerant long-running applications with AWS Lambda Durable Functions](https://aws.amazon.com/vi/blogs/compute/building-fault-tolerant-long-running-application-with-aws-lambda-durable-functions/)
- [AWS Lambda Durable Functions](https://aws.amazon.com/vi/lambda/lambda-durable-functions/)
- [Lambda durable multi-step applications and AI workflows](https://aws.amazon.com/vi/about-aws/whats-new/2025/12/lambda-durable-multi-step-applications-ai-workflows/)
- [Durable Execution SDK documentation](https://docs.aws.amazon.com/lambda/latest/dg/durable-execution-sdk.html)
