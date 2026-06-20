---
title: "Nhật Ký Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

## Tuần 3 - Vận hành EC2 nâng cao, RDS, S3 & CloudWatch

### Chủ đề tuần

Thao tác EC2 nâng cao + RDS + S3 static hosting + giám sát CloudWatch

### Mục tiêu tuần

* Hoàn thành các thao tác nâng cao trên EC2: thay đổi kích thước, snapshots, AMI, triển khai ứng dụng.
* Tìm hiểu Amazon RDS, Amazon S3 static hosting, và giám sát CloudWatch.

### Lịch công việc:
| Ngày | Thứ | Công việc | Lab / Dự án |
| --- | --- | --- | --- |
| 04/05/2026 | Thứ 2 | Thay đổi instance type của EC2.<br>Tạo và quản lý EBS snapshots.<br>Tạo custom AMI và khởi tạo instances từ AMI đó.<br>Khôi phục quyền truy cập vào Linux và Windows instances, sau đó hoàn thành phần nâng cao của Lab 000004. | [Lab 000004 - Giới thiệu Amazon EC2](https://000004.awsstudygroup.com/) |
| 05/05/2026 | Thứ 3 | Cài đặt LAMP server và Node.js trên Amazon Linux 2023.<br>Triển khai ứng dụng Node.js trên EC2 cho cả Linux và Windows.<br>Ôn lại AWS CLI cơ bản cho EC2, S3 và IAM, đồng thời tạo AWS Budgets alert.<br>Thực hành các lab liên quan đến triển khai và terminate EC2 instances cuối ngày. | [Lab 000004 - Giới thiệu Amazon EC2](https://000004.awsstudygroup.com/) |
| 06/05/2026 | Thứ 4 | Tạo VPC và security group cho Amazon RDS.<br>Khởi tạo RDS MySQL managed instance và triển khai ứng dụng kết nối tới đó.<br>Thực hành backup và restore với RDS snapshots.<br>Thực hành Lab 000005. | [Lab 000005 - Kiến thức cơ sở dữ liệu với Amazon RDS](https://000005.awsstudygroup.com/) |
| 07/05/2026 | Thứ 5 | Tạo S3 bucket và cấu hình public access để host static website.<br>Upload các file HTML/CSS và cấu hình bucket policy cùng versioning.<br>Kiểm tra pre-signed URLs cho truy cập có kiểm soát.<br>Thực hành Lab 000057 và dọn dẹp tài nguyên cuối tuần. | [Lab 000057 - Lưu trữ website tĩnh với Amazon S3](https://000057.awsstudygroup.com/) |
| 08/05/2026 | Thứ 6 | Tìm hiểu CloudWatch metrics và dashboards.<br>Thiết lập alarm CPU > 80% kèm SNS email notification.<br>Cấu hình log groups, Log Insights và CloudWatch Agent trên EC2.<br>Thực hành Lab 000008. | [Lab 000008 - Giám sát với Amazon CloudWatch](https://000008.awsstudygroup.com/) |


### Kết quả kỳ vọng

* Thành thạo các thao tác EC2 nâng cao như resize, snapshots, tạo AMI và khôi phục quyền truy cập.
* Triển khai workload ứng dụng trên EC2 và dùng AWS CLI cho các tác vụ vận hành cơ bản.
* Khởi tạo và vận hành được Amazon RDS MySQL managed instance kèm thực hành backup, restore.
* Host static website trên Amazon S3 với access control và versioning phù hợp.
* Cấu hình giám sát Amazon CloudWatch với alarms, logs và CloudWatch Agent.

### Tham chiếu tuần 3

* [Lab 000004 - Kiến thức tính toán cơ bản với Amazon EC2](https://000004.awsstudygroup.com/)
* [Lab 000005 - Kiến thức cơ sở dữ liệu với Amazon RDS](https://000005.awsstudygroup.com/)
* [Lab 000057 - Lưu trữ website tĩnh với Amazon S3](https://000057.awsstudygroup.com/)
* [Lab 000008 - Giám sát với Amazon CloudWatch](https://000008.awsstudygroup.com/)

