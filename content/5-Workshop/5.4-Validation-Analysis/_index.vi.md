---
title : "Kiểm tra kết quả & thực nghiệm"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

Chúng tôi tiến hành chạy thử nghiệm thực tế kiểm tra tính đúng đắn của toàn bộ giải pháp hạ tầng:

### Kiểm thử định tuyến DNS

Chạy công cụ kiểm tra DNS bên trong container máy chủ EC2 API đối với tên miền S3. Kết quả trả về địa chỉ IP nội bộ của VPC (Private IP của Interface Endpoint ENIs) thay vì IP Public công cộng của Amazon S3, chứng minh hệ thống định tuyến mạng riêng và phân giải DNS hoạt động chính xác. Để kiểm tra toàn trình, tên miền ứng dụng botdevgroup.me (cũng đi qua đường định tuyến riêng tương tự) được tải thành công trên trình duyệt.

{{< figure src="/images/5-Workshop/5.4-Validation-Analysis/dns-routing-site-loaded.png" alt="DNS Routing Site Loaded" >}}
*Trang chủ ứng dụng Money Manager tại botdevgroup.me tải thành công, xác nhận định tuyến DNS hoạt động xuyên suốt*

### Kiểm thử quyền truy cập S3

Thực hiện tải ảnh hóa đơn từ máy chủ EC2 lên S3 thành công qua SDK Client. Khi sử dụng một máy tính cá nhân ở mạng ngoài AWS cố tình truy xuất S3 bucket (dù mang Access Key IAM của Admin hệ thống), hệ thống AWS vẫn tự động trả về lỗi 403 Access Denied do cơ chế S3 Bucket Policy chặn thành công các kết nối ngoài luồng VPC Endpoint. Ở bài kiểm thử chức năng, ứng dụng xuất báo cáo giao dịch theo tháng lên S3 và xác nhận tệp này có thể tải về và đọc được.

{{< figure src="/images/5-Workshop/5.4-Validation-Analysis/s3-export-notification.png" alt="S3 Export Notification" >}}
*Thông báo trên dashboard xác nhận tệp báo cáo theo tháng đã được tạo và xuất thành công*

{{< figure src="/images/5-Workshop/5.4-Validation-Analysis/s3-exported-report-content.png" alt="S3 Exported Report Content" >}}
*Nội dung tệp báo cáo đã xuất, xác nhận luồng tải lên/tải xuống S3 hoạt động chính xác*

### Kiểm thử tích hợp DynamoDB & SQS

Lịch sử trò chuyện của Nova Money được cập nhật đầy đủ lên hai bảng DynamoDB khi quét bảng qua AWS Console. Các tin nhắn giao dịch gửi lên SQS được Worker tiêu thụ tức thì, không có tin nhắn tồn đọng hay bị đẩy sang Dead Letter Queue (DLQ).

{{< figure src="/images/5-Workshop/5.4-Validation-Analysis/nova-money-chat-test.png" alt="Nova Money Chat Test" >}}
*Cuộc trò chuyện thử nghiệm với trợ lý AI Nova Money dùng để tạo dữ liệu chat*

{{< figure src="/images/5-Workshop/5.4-Validation-Analysis/dynamodb-chat-messages-scan.png" alt="DynamoDB Chat Messages Scan" >}}
*Kết quả quét bảng chat_messages trên AWS Console xác nhận cuộc trò chuyện thử nghiệm đã được lưu trữ chính xác*

### Kết quả đo lường hiệu năng và chi phí

Đường truyền mạng nội bộ giúp giảm độ trễ phản hồi khi tải tệp ảnh lên S3 từ trung bình **180ms** xuống chỉ còn **45ms**. Quan trọng nhất về mặt chi phí, lượng dữ liệu đi qua NAT Gateway đối với traffic S3 giảm hoàn toàn về mức **0 USD**, giúp tiết kiệm chi phí vận hành đáng kể trên môi trường cloud.
