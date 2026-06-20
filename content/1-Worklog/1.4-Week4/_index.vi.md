---
title: "Nhật Ký Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

## Tuần 4 - Auto Scaling, Route 53, DynamoDB, CloudFront & Kiến trúc HA

### Chủ đề tuần

Auto Scaling + Route 53 + DynamoDB + CloudFront + kiến trúc high availability

### Mục tiêu tuần

* Tìm hiểu EC2 Auto Scaling, Application Load Balancer, Route 53 DNS, DynamoDB, CloudFront, và kiến trúc High Availability.

### Lịch công việc:
| Ngày | Thứ | Công việc | Lab / Dự án |
| --- | --- | --- | --- |
| 11/05/2026 | Thứ 2 | Tạo launch template và Auto Scaling Group.<br>Cấu hình target tracking scaling policy.<br>Thiết lập Application Load Balancer với listener rules.<br>Kiểm tra scale-out, scale-in và health check trong Lab 000006. | [Lab 000006 - Mở rộng ứng dụng với EC2 Auto Scaling](https://000006.awsstudygroup.com/) |
| 12/05/2026 | Thứ 3 | Tìm hiểu Route 53 hosted zone và các record type phổ biến như A, CNAME, Alias.<br>Cấu hình các routing policy cơ bản.<br>Thiết lập mô hình hybrid DNS tích hợp với VPC.<br>Thực hành Lab 000010. | [Lab 000010 - Quản lý Hybrid DNS với Amazon Route 53](https://000010.awsstudygroup.com/) |
| 13/05/2026 | Thứ 4 | Tạo bảng DynamoDB với thiết kế partition key và sort key.<br>Thực hiện CRUD qua console và CLI.<br>Cấu hình Global Secondary Index và so sánh on-demand với provisioned capacity.<br>Thực hành Lab 000060 và dọn dẹp tài nguyên. | [Lab 000060 - Kiến thức NoSQL cơ bản với Amazon DynamoDB](https://000060.awsstudygroup.com/) |
| 14/05/2026 | Thứ 5 | Tìm hiểu CloudFront gồm distribution, origin và cache behaviors.<br>Tích hợp CloudFront với static website trên S3.<br>Cấu hình HTTPS với ACM và thực hiện cache invalidation.<br>Thực hành Lab 000094. | [Lab 000094 - Phân phối nội dung với CloudFront](https://000094.awsstudygroup.com/) |
| 15/05/2026 | Thứ 6 | Thiết kế kiến trúc Multi-AZ sử dụng ALB, EC2 và RDS.<br>Cấu hình target groups và listener rules.<br>Triển khai RDS Multi-AZ và kiểm tra health check cùng failover behavior.<br>Thực hành Lab 000101. | [Lab 000101 - Xây dựng ứng dụng web High Availability](https://000101.awsstudygroup.com/) |


### Kết quả kỳ vọng

* Hiểu cách EC2 Auto Scaling, ALB và scaling policies phối hợp trong kiến trúc co giãn.
* Cấu hình được Route 53 DNS records và các chiến lược định tuyến cơ bản, bao gồm hybrid DNS.
* Làm việc với thiết kế bảng DynamoDB, CRUD operations, secondary indexes và capacity models.
* Dùng CloudFront để phân phối nội dung từ S3 an toàn qua HTTPS với cache management.
* Xây dựng và kiểm chứng kiến trúc web Multi-AZ có tính high availability bằng ALB, EC2 và RDS.

### Tham chiếu tuần 4

* [Lab 000006 - Mở rộng ứng dụng với EC2 Auto Scaling](https://000006.awsstudygroup.com/)
* [Lab 000010 - Quản lý Hybrid DNS với Amazon Route 53](https://000010.awsstudygroup.com/)
* [Lab 000060 - Kiến thức NoSQL cơ bản với Amazon DynamoDB](https://000060.awsstudygroup.com/)
* [Lab 000094 - Phân phối nội dung với Amazon CloudFront](https://000094.awsstudygroup.com/)
* [Lab 000101 - Xây dựng ứng dụng web High Availability](https://000101.awsstudygroup.com/)


