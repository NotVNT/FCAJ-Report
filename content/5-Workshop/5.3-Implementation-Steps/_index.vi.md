---
title : "Các bước thực hiện chi tiết"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### Bước 1: Thiết lập mạng riêng VPC và máy chủ EC2

Quy trình xây dựng môi trường mạng cô lập và máy chủ tính toán cốt lõi:

- Khởi tạo một **VPC** có dải IP CIDR là `10.0.0.0/16` làm dải mạng riêng tư chính.

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/vpc-list.png" alt="Danh sách VPC hiển thị VPC tùy chỉnh với dải CIDR 10.0.0.0/16" link="/images/5-Workshop/5.3-Implementation-Steps/vpc-list.png" caption="Hình 3. Danh sách VPC hiển thị VPC tùy chỉnh với dải CIDR 10.0.0.0/16" >}}

- Phân chia mạng con thành **Public Subnets** (nơi ALB và NAT Gateway cư trú để có thể tiếp xúc trực tiếp với Internet công cộng) và **Private Subnets** (nơi đặt máy chủ EC2 API và Worker để cô lập hoàn toàn khỏi Internet Gateway).

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/subnets-list.png" alt="Danh sách 6 Subnets được phân bổ giữa hai tầng Public và Private" link="/images/5-Workshop/5.3-Implementation-Steps/subnets-list.png" caption="Hình 4. Danh sách 6 Subnets được phân bổ giữa hai tầng Public và Private" >}}

- Cấu hình các bảng định tuyến (**Route Tables**) tương ứng cho Public Subnet hướng ra ngoài Internet Gateway, và Private Subnet định tuyến outbound ra ngoài thông qua NAT Gateway đặt ở Public Subnet.
- Triển khai máy chủ EC2 kích thước `t3.micro` trong Private Subnet chạy hệ điều hành **Amazon Linux 2023**. Tiến hành cài đặt **Docker** và **Docker Compose** để quản lý và vận hành ứng dụng backend Spring Boot.

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/ec2-instances-list.png" alt="Danh sách EC2 Instances cho thấy moneymanager-app đang ở trạng thái Running" link="/images/5-Workshop/5.3-Implementation-Steps/ec2-instances-list.png" caption="Hình 5. Danh sách EC2 Instances cho thấy moneymanager-app đang ở trạng thái Running" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/ec2-instance-detail.png" alt="Trang chi tiết EC2 instance moneymanager-app hiển thị địa chỉ Private IP" link="/images/5-Workshop/5.3-Implementation-Steps/ec2-instance-detail.png" caption="Hình 6. Trang chi tiết EC2 instance moneymanager-app hiển thị địa chỉ Private IP" >}}

- Backend Spring Boot được chia tách thành hai container chạy độc lập: container `moneymanager-api` đảm nhận nhiệm vụ phản hồi các yêu cầu HTTP/REST API trên cổng `8080` (ALB sẽ nhận traffic HTTPS từ ngoài và chuyển tiếp về đây), và container `moneymanager-worker` chịu trách nhiệm tiêu thụ tin nhắn từ hàng đợi SQS và thực hiện các tác vụ nền định kỳ mà không mở bất kỳ cổng kết nối nào ra ngoài.
- Tệp cấu hình môi trường `/app/.env` được lưu trữ trực tiếp trên phân vùng ổ đĩa EBS của máy chủ EC2 để bảo mật thông tin và tiêm các biến môi trường trực tiếp vào các container khi khởi chạy.

### Bước 2: Cấu hình cơ sở dữ liệu RDS MySQL và ElastiCache Redis

Triển khai phân hệ lưu trữ dữ liệu quan hệ và bộ nhớ đệm tốc độ cao:

- Khởi tạo một cơ sở dữ liệu **RDS MySQL 8.0**, kích thước `db.t3.micro`. Cơ sở dữ liệu này được đặt trong một Subnet Group bao gồm các Private Subnet của VPC để ngăn chặn hoàn toàn khả năng tiếp cận từ bên ngoài.

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/rds-databases-list.png" alt="Danh sách RDS Databases với instance db-moneymanager MySQL 8.0" link="/images/5-Workshop/5.3-Implementation-Steps/rds-databases-list.png" caption="Hình 7. Danh sách RDS Databases với instance db-moneymanager MySQL 8.0" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/rds-instance-detail.png" alt="Trang chi tiết RDS instance, tab Connectivity & security" link="/images/5-Workshop/5.3-Implementation-Steps/rds-instance-detail.png" caption="Hình 8. Trang chi tiết RDS instance, tab Connectivity & security" >}}

- Nhóm bảo mật (**Security Group**) của RDS MySQL được thiết lập chế độ chặn hoàn toàn, chỉ cho phép các yêu cầu truy vấn TCP bắt nguồn từ nhóm bảo mật của máy chủ EC2 API trên cổng mặc định `3306`. Kết nối từ máy API sử dụng cơ chế **Hibernate JPA** để tự động cập nhật cấu trúc bảng dữ liệu (schema) dựa trên các thực thể Java (Entity classes).
- Khởi tạo cụm bộ nhớ đệm **ElastiCache Redis** kích thước node `cache.t3.micro` chạy trong phân vùng Private Subnet. Nhóm bảo mật của Redis được cấu hình chỉ chấp nhận các kết nối mạng nội bộ trên cổng `6379` từ EC2 API.

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/elasticache-redis-list.png" alt="Danh sách ElastiCache Redis OSS caches với cụm moneymanager-redis" link="/images/5-Workshop/5.3-Implementation-Steps/elasticache-redis-list.png" caption="Hình 9. Danh sách ElastiCache Redis OSS caches với cụm moneymanager-redis" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/elasticache-cluster-detail.png" alt="Trang chi tiết cụm ElastiCache moneymanager-redis" link="/images/5-Workshop/5.3-Implementation-Steps/elasticache-cluster-detail.png" caption="Hình 10. Trang chi tiết cụm ElastiCache moneymanager-redis" >}}

- Spring Boot API sử dụng Redis làm tầng cache dữ liệu đệm cho các tài nguyên ít thay đổi nhằm giảm tải truy vấn IO cho MySQL, đồng thời chạy thuật toán giới hạn tần suất (Rate Limiting) cho các cuộc hội thoại chat AI của trợ lý **Nova Money** nhằm ngăn chặn hành vi tấn công spam làm cạn kiệt API key.

### Bước 3: Tích hợp Amazon DynamoDB và AWS SQS

Thiết lập kho lưu trữ phi cấu trúc NoSQL và hệ thống hàng đợi tin nhắn điều phối sự kiện:

- Trên trang **DynamoDB Console**, khởi tạo hai bảng dữ liệu chính với chế độ năng lực theo yêu cầu (**On-Demand Capacity Mode**): bảng `chat_sessions` lưu trữ thông tin phiên trò chuyện (Partition key: `id` kiểu String) và bảng `chat_messages` lưu trữ chi tiết lịch sử tin nhắn (Partition key: `id` kiểu String).

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/dynamodb-tables-list.png" alt="Danh sách DynamoDB Tables gồm chat_messages và chat_sessions" link="/images/5-Workshop/5.3-Implementation-Steps/dynamodb-tables-list.png" caption="Hình 11. Danh sách DynamoDB Tables gồm chat_messages và chat_sessions" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/dynamodb-chat-messages-detail.png" alt="Trang chi tiết bảng chat_messages" link="/images/5-Workshop/5.3-Implementation-Steps/dynamodb-chat-messages-detail.png" caption="Hình 12. Trang chi tiết bảng chat_messages" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/dynamodb-chat-sessions-detail.png" alt="Trang chi tiết bảng chat_sessions" link="/images/5-Workshop/5.3-Implementation-Steps/dynamodb-chat-sessions-detail.png" caption="Hình 13. Trang chi tiết bảng chat_sessions" >}}

- Gán quyền đọc/ghi DynamoDB cho EC2 thông qua **IAM Instance Profile**. Trong mã nguồn Spring Boot backend, loại bỏ thư viện kết nối MongoDB Atlas cũ, tích hợp thư viện **SDK AWS v2** cho DynamoDB, cấu hình bean `DynamoDbClient` trỏ tới vùng hạ tầng Singapore để lưu lịch sử hội thoại của trợ lý ảo Nova Money một cách nhanh chóng và tối ưu chi phí.
- Khởi tạo hàng đợi tiêu chuẩn **AWS SQS** mang tên `moneymanager-async-jobs`. Để xử lý các tin nhắn bị lỗi sau nhiều lần xử lý lại, cấu hình một hàng đợi phụ **Dead Letter Queue (DLQ)** tên là `moneymanager-async-jobs-dlq` liên kết với hàng đợi chính qua chính sách Redrive Policy thử lại tối đa 3 lần.

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/sqs-queues-list.png" alt="Danh sách SQS Queues gồm moneymanager-async-jobs và DLQ tương ứng" link="/images/5-Workshop/5.3-Implementation-Steps/sqs-queues-list.png" caption="Hình 14. Danh sách SQS Queues gồm moneymanager-async-jobs và DLQ tương ứng" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/sqs-main-queue-detail.png" alt="Trang chi tiết hàng đợi chính moneymanager-async-jobs" link="/images/5-Workshop/5.3-Implementation-Steps/sqs-main-queue-detail.png" caption="Hình 15. Trang chi tiết hàng đợi chính moneymanager-async-jobs" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/sqs-dlq-detail.png" alt="Trang chi tiết Dead Letter Queue moneymanager-async-jobs-dlq" link="/images/5-Workshop/5.3-Implementation-Steps/sqs-dlq-detail.png" caption="Hình 16. Trang chi tiết Dead Letter Queue moneymanager-async-jobs-dlq" >}}

- Trong ứng dụng backend, khi người dùng thực hiện giao dịch tài chính lớn, container API sẽ serialize dữ liệu sự kiện thành chuỗi JSON và dùng đối tượng `SqsTemplate` đẩy sự kiện vào SQS. Container Worker sử dụng chú thích `@SqsListener` để lắng nghe SQS và thực thi xử lý bất đồng bộ các công việc như gửi mail thông báo và tính toán lại giới hạn hũ ngân sách mà không ảnh hưởng tới thời gian phản hồi API của người dùng.
- IAM Role gắn cho máy chủ EC2 chỉ được cấp đúng các quyền SQS cần thiết, tuân theo nguyên tắc phân quyền tối thiểu (least-privilege):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "sqs:SendMessage",
        "sqs:ReceiveMessage",
        "sqs:DeleteMessage",
        "sqs:GetQueueAttributes"
      ],
      "Resource": "arn:aws:sqs:ap-southeast-1:123456789012:moneymanager-async-jobs"
    }
  ]
}
```

### Bước 4: Thiết lập Bảo mật Amazon S3 và VPC Endpoints

Thiết lập kết nối mạng riêng tối ưu hóa độ trễ và chi phí kết nối đến S3:

- Khởi tạo **Amazon S3 Bucket** mang tên `botdevgroup-documents` ở chế độ riêng tư hoàn toàn (**Block Public Access**) và bật tính năng mã hóa dữ liệu **SSE-S3**.

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/s3-buckets-list.png" alt="Danh sách S3 Buckets gồm botdevgroup-documents và bucket lưu trang web tĩnh của dự án" link="/images/5-Workshop/5.3-Implementation-Steps/s3-buckets-list.png" caption="Hình 17. Danh sách S3 Buckets gồm botdevgroup-documents và bucket lưu trang web tĩnh của dự án" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/s3-documents-bucket-objects.png" alt="Các đối tượng lưu trữ trong bucket botdevgroup-documents" link="/images/5-Workshop/5.3-Implementation-Steps/s3-documents-bucket-objects.png" caption="Hình 18. Các đối tượng lưu trữ trong bucket botdevgroup-documents" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/s3-website-bucket-objects.png" alt="Các đối tượng lưu trữ trong bucket trang web tĩnh botdevgroup.me" link="/images/5-Workshop/5.3-Implementation-Steps/s3-website-bucket-objects.png" caption="Hình 19. Các đối tượng lưu trữ trong bucket trang web tĩnh botdevgroup.me" >}}

- Tạo một **Gateway VPC Endpoint** cho S3 và gán vào Route Table của các Private Subnets trong VPC. Dòng định tuyến mới được tự động thêm vào sẽ hướng toàn bộ các yêu cầu từ EC2 kết nối tới S3 đi qua mạng trục nội bộ của AWS thay vì truyền qua NAT Gateway ra Internet, giúp cắt giảm 100% chi phí xử lý băng thông trên NAT Gateway đối với lưu lượng S3 và tăng tốc độ truyền tải tệp. Endpoint được khởi tạo bằng lệnh AWS CLI và gán trực tiếp vào Route Table của Private Subnets:

```bash
aws ec2 create-vpc-endpoint \
  --vpc-id vpc-0123456789abcdef0 \
  --vpc-endpoint-type Gateway \
  --service-name com.amazonaws.ap-southeast-1.s3 \
  --route-table-ids rtb-0123456789abcdef0
```

- Tạo một **Interface VPC Endpoint (AWS PrivateLink)** trong các Private Subnet thuộc hai Availability Zone khác nhau để đảm bảo tính dự phòng cao. Interface Endpoint này sẽ cấp phát các địa chỉ IP nội bộ riêng từ VPC.

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/vpc-dashboard-list.png" alt="Trang dashboard VPC liệt kê các VPC dùng để cấu hình Interface Endpoint PrivateLink" link="/images/5-Workshop/5.3-Implementation-Steps/vpc-dashboard-list.png" caption="Hình 20. Trang dashboard VPC liệt kê các VPC dùng để cấu hình Interface Endpoint PrivateLink" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/vpc-resource-map.png" alt="Sơ đồ tài nguyên (Resource map) của botdevgroup-vpc thể hiện các Subnet, Route Table và kết nối Endpoint" link="/images/5-Workshop/5.3-Implementation-Steps/vpc-resource-map.png" caption="Hình 21. Sơ đồ tài nguyên (Resource map) của botdevgroup-vpc thể hiện các Subnet, Route Table và kết nối Endpoint" >}}

- Cấu hình một **Inbound Resolver** trong dịch vụ DNS **Route 53** để lắng nghe yêu cầu từ mạng ngoài (văn phòng kết nối VPN) truyền tới, phân giải tên miền công cộng của S3 về địa chỉ IP nội bộ của Interface Endpoint ENIs, giúp các máy trạm tại văn phòng upload hóa đơn hay tải báo cáo qua VPN an toàn.
- Cấu hình chính sách **Endpoint Policy** tại hai VPC Endpoint vừa tạo để quy định chỉ cho phép các thao tác upload/read hướng tới duy nhất S3 Bucket của dự án Money Manager, ngăn chặn việc rò rỉ dữ liệu ra ngoài. Đồng thời, cấu hình chính sách **S3 Bucket Policy** từ chối tuyệt đối mọi yêu cầu truy xuất S3 từ bên ngoài nếu không đi qua hai VPC Endpoint hợp lệ của hệ thống.

### Bước 5: Cấu hình giám sát và cảnh báo với Amazon CloudWatch

Thiết lập hệ thống giám sát tập trung cho cụm máy chủ EC2 API/Worker và các dịch vụ phụ thuộc:

- Cấu hình **Log Appender** trong ứng dụng Spring Boot (sử dụng thư viện AWS Logback Appender) để tự động đẩy nhật ký hoạt động (logs) của container API và Worker về CloudWatch Log Group `/aws/ec2/moneymanager-app`. Nhật ký lỗi của RDS MySQL (`/aws/rds/moneymanager-db`) và lưu lượng mạng VPC (`/aws/vpc/flow-logs`) cũng được đẩy về các Log Group riêng, giúp tập trung theo dõi toàn bộ hệ thống tại một nơi.

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/cloudwatch-log-groups-list.png" alt="Danh sách CloudWatch Log Groups gồm /aws/ec2/moneymanager-app, /aws/rds/moneymanager-db và /aws/vpc/flow-logs đang nhận log liên tục" link="/images/5-Workshop/5.3-Implementation-Steps/cloudwatch-log-groups-list.png" caption="Hình 22. Danh sách CloudWatch Log Groups gồm /aws/ec2/moneymanager-app, /aws/rds/moneymanager-db và /aws/vpc/flow-logs đang nhận log liên tục" >}}

- Thiết lập bộ lọc chỉ số (**Metric Filter**) mang tên `EC2ErrorFilter` trên Log Group `/aws/ec2/moneymanager-app` để quét qua các luồng log và đếm tần suất xuất hiện các lỗi nghiêm trọng (khớp mẫu như `ERROR` hoặc `Exception`), phát ra chỉ số tùy chỉnh `EC2ErrorCount`. Một bộ lọc tương tự mang tên `RDSLogErrorFilter` cũng được cấu hình trên `/aws/rds/moneymanager-db` để theo dõi tần suất lỗi ở tầng cơ sở dữ liệu.

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/cloudwatch-ec2-metric-filter-detail.png" alt="Chi tiết Metric Filter EC2ErrorFilter trên log group /aws/ec2/moneymanager-app, liên kết với alarm EC2ErrorAlarm" link="/images/5-Workshop/5.3-Implementation-Steps/cloudwatch-ec2-metric-filter-detail.png" caption="Hình 23. Chi tiết Metric Filter EC2ErrorFilter trên log group /aws/ec2/moneymanager-app, liên kết với alarm EC2ErrorAlarm" >}}

{{< figure src="/images/5-Workshop/5.3-Implementation-Steps/cloudwatch-rds-metric-filter-detail.png" alt="Chi tiết Metric Filter RDSLogErrorFilter trên log group /aws/rds/moneymanager-db" link="/images/5-Workshop/5.3-Implementation-Steps/cloudwatch-rds-metric-filter-detail.png" caption="Hình 24. Chi tiết Metric Filter RDSLogErrorFilter trên log group /aws/rds/moneymanager-db" >}}

- Cấu hình **CloudWatch Alarm** mang tên `EC2ErrorAlarm` dựa trên chỉ số `EC2ErrorCount`, chuyển sang trạng thái `ALARM` khi số lượng lỗi đạt từ 1 trở lên trong vòng 5 phút, tự động gửi thông báo qua SNS.

```xml
<!-- logback-spring.xml -->
<configuration>
    <appender name="CLOUDWATCH" class="ca.pjer.logback.AwsLogsAppender">
        <groupName>/aws/ec2/moneymanager-app</groupName>
        <streamName>backend-logs</streamName>
        <regionName>ap-southeast-1</regionName>
        <layout>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </layout>
    </appender>

    <root level="INFO">
        <appender-ref ref="CLOUDWATCH" />
    </root>
</configuration>
```

> Xem sơ đồ kiến trúc tổng thể tại mục **5.1. Giới thiệu** để hiểu rõ hơn cách các thành phần này liên kết với nhau.
