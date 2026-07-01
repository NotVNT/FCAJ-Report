---
title : "Test Results & Experimentation"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

We conducted real-world testing to verify the correctness of the entire infrastructure solution:

### DNS Routing Test

Ran DNS lookup tools inside the EC2 API server container for the S3 domain. The result returned the VPC's internal IP address (Private IP of Interface Endpoint ENIs) instead of Amazon S3's public IP, proving that the private network routing and DNS resolution system works correctly. For an end-to-end test, the application domain botdevgroup.me (also routed through the same private path) loaded successfully in the browser.

![DNS Routing Site Loaded](/images/5-Workshop/5.4-Validation-Analysis/dns-routing-site-loaded.png)
*Money Manager application homepage at botdevgroup.me loaded successfully, confirming end-to-end DNS routing works*

### S3 Access Permissions Test

Successfully uploaded invoice images from the EC2 server to S3 via the SDK Client. When using a personal computer outside the AWS network attempting to access the S3 bucket (even with an Admin IAM Access Key), AWS automatically returned a 403 Access Denied error because the S3 Bucket Policy successfully blocked connections outside the VPC Endpoint flow. In the functional test, the application exported monthly transaction reports to S3 and confirmed the file could be downloaded and read.

![S3 Export Notification](/images/5-Workshop/5.4-Validation-Analysis/s3-export-notification.png)
*Dashboard notification confirming the monthly report was successfully created and exported*

![S3 Exported Report Content](/images/5-Workshop/5.4-Validation-Analysis/s3-exported-report-content.png)
*Content of the exported report, confirming the S3 upload/download flow works correctly*

### DynamoDB & SQS Integration Test

Nova Money's chat history was fully updated in both DynamoDB tables when scanned via the AWS Console. Transaction messages sent to SQS were immediately consumed by the Worker, with no backlog or messages pushed to the Dead Letter Queue (DLQ).

![Nova Money Chat Test](/images/5-Workshop/5.4-Validation-Analysis/nova-money-chat-test.png)
*Test conversation with Nova Money AI assistant used to generate chat data*

![DynamoDB Chat Messages Scan](/images/5-Workshop/5.4-Validation-Analysis/dynamodb-chat-messages-scan.png)
*DynamoDB chat_messages table scan results on AWS Console confirming the test conversation was accurately stored*

### Performance and Cost Measurement Results

The internal network path reduced upload latency for image files to S3 from an average of **180ms** down to just **45ms**. Most importantly in terms of cost, the amount of data passing through the NAT Gateway for S3 traffic completely dropped to **$0 USD**, delivering significant operational cost savings on the cloud environment.
