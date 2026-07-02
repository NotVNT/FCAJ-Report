---
title : "Introduction"
date : 2024-01-01 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

### Deploy Infrastructure and Secure Connection to Amazon S3

{{< figure src="/images/5-Workshop/5.1-Introduction/architecture-diagram.png" alt="architecture" caption="Figure 1. Overall network infrastructure architecture and AWS service integration" >}}

### Introduction Overview

This lab fully documents the process of building and testing cloud infrastructure for the Money Manager personal finance management project.

The workshop focuses on:

+ Setting up a secure private network subsystem (VPC).
+ Configuring separation of API application servers and Workers.
+ Deploying data storage services: MySQL RDS, Redis ElastiCache, DynamoDB.
+ Configuring SQS asynchronous queues.
+ Optimizing network traffic using VPC Endpoints to Amazon S3 to protect OCR invoice images from information leakage risks over the public Internet and reduce NAT Gateway costs.
+ Through this hands-on practice, we gained exposure to system design methodology following the AWS Well-Architected Framework, with particular emphasis on two pillars: Security and Cost Optimization.
