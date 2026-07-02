---
title : "Kiểm tra kết quả & thực nghiệm"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

Chúng tôi tiến hành chạy thử nghiệm thực tế để kiểm tra tính đúng đắn và hiệu năng của toàn bộ giải pháp hạ tầng đã triển khai, bao gồm định tuyến DNS riêng qua VPC Endpoints, kiểm soát quyền truy cập S3, tích hợp DynamoDB/SQS, giám sát CloudWatch và hành vi tổng thể của ứng dụng chạy trực tiếp trên backend EC2/ALB.

### Video trải nghiệm ứng dụng Web

Video dưới đây trình bày toàn bộ luồng hoạt động của ứng dụng Web trên hạ tầng đã triển khai: định tuyến DNS đến S3 qua endpoint riêng, xuất/tải báo cáo giao dịch tháng qua S3, trợ lý AI Nova Money với lịch sử chat lưu trên DynamoDB, xử lý giao dịch bất đồng bộ qua SQS, và dashboard giám sát CloudWatch.

{{< youtube oCs0s21PJMw >}}

### Kiểm thử Mobile

