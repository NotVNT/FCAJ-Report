---
title : "Clean up"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

After completing the lab session, clean up all test infrastructure resources to avoid incurring ongoing charges on your AWS account:

1. Delete all test image files uploaded to the **botdevgroup-documents** S3 bucket to avoid monthly storage fees.
2. Delete the **Interface VPC Endpoint** vpce-s3-interface to release the Network Interfaces and stop hourly charges for AWS PrivateLink.
3. Detach the **Gateway VPC Endpoint** vpce-s3-gateway from the Private Subnets Route Table to restore the original VPC routing configuration.
4. Delete Security Groups and test DNS records on Route 53 Resolver.
5. Run the Docker cache cleanup command (`docker system prune -af`) on the EC2 server to free up EBS disk space.
