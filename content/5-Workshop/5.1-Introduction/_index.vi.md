---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### Triển khai hạ tầng và kết nối bảo mật đến Amazon S3

{{< figure src="/images/5-Workshop/5.1-Introduction/architecture-diagram.png" alt="architecture" >}}
*Hình 1. Sơ đồ kiến trúc tổng thể hạ tầng mạng và tích hợp dịch vụ AWS*

### Giới thiệu tổng quan

Bài thực hành này tài liệu hóa đầy đủ quy trình xây dựng và kiểm thử hệ thống hạ tầng đám mây cho dự án quản lý tài chính cá nhân Money Manager.

Nội dung workshop tập trung vào:

+ Thiết lập phân hệ mạng riêng tư bảo mật (VPC).
+ Cấu hình phân tách máy chủ ứng dụng API và Worker.
+ Triển khai các dịch vụ lưu trữ dữ liệu: MySQL RDS, Redis ElastiCache, DynamoDB.
+ Cấu hình hàng đợi bất đồng bộ SQS.
+ Tối ưu hóa đường truyền mạng bằng VPC Endpoints đến Amazon S3 để bảo vệ ảnh hóa đơn OCR khỏi các rủi ro rò rỉ thông tin qua Internet công cộng và cắt giảm chi phí NAT Gateway.
+ Thông qua quá trình thực hành thực tế này, chúng tôi đã tiếp cận được phương pháp thiết kế hệ thống theo tiêu chuẩn AWS Well-Architected Framework, đặc biệt nhấn mạnh vào hai trụ cột: Bảo mật (Security) và Tối ưu hóa chi phí (Cost Optimization).
