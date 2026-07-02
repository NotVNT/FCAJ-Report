---
title : "Các bước chuẩn bị"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

### Tài khoản và Quyền truy cập

Một tài khoản AWS hoạt động với quyền quản trị viên IAM. Để có khóa bảo mật kết nối từ máy trạm, chúng tôi thực hiện các bước sau:

**Bước 1 (Trên AWS Console):** Đăng nhập vào AWS Management Console, truy cập dịch vụ IAM (Identity and Access Management) -> Users, chọn tên người dùng của mình, chuyển sang tab Security credentials và tìm đến mục Access keys. Nhấp vào nút Create access key, chọn mục đích sử dụng là Command Line Interface (CLI), đồng ý các điều khoản và bấm xác nhận tạo để hệ thống sinh ra cặp khóa bao gồm Access Key ID và Secret Access Key. Tải xuống tệp tin dạng .csv để lưu trữ khóa bảo mật này.

**Bước 2 (Tại máy trạm):** Mở Terminal/Powershell trên máy tính cá nhân và chạy lệnh cấu hình `aws configure`. Nhập thông tin Access Key ID và Secret Access Key đã khởi tạo ở Bước 1, nhập Default region name là `ap-southeast-1` (Singapore) và Default output format là `json`. Cấu hình này sẽ được lưu tự động tại thư mục cá nhân của người dùng (tệp tin credentials và config tại đường dẫn `%USERPROFILE%\.aws\` trên Windows hoặc `~/.aws/` trên Linux/macOS).

{{< figure src="/images/5-Workshop/5.2-Prerequisite/iam-access-key-creation.png" alt="IAM Access Key" caption="Tab Security credentials của IAM với mục Access keys dùng để tạo khóa kết nối CLI" >}}

### Môi trường máy trạm local

Đảm bảo máy trạm đã cài đặt thành công môi trường **Node.js** phiên bản 20 trở lên, **Java Development Kit (JDK)** phiên bản 21, công cụ build **Maven**, và **Docker Desktop** để thực hiện đóng gói và kiểm thử cục bộ trước khi đẩy hình ảnh Docker lên ECR. Môi trường local cần được kết nối ổn định với Internet để tải các thư viện Maven và Docker Base Images liên quan.

### Xác định vùng hạ tầng

Lựa chọn Vùng hạ tầng mạng AWS tại khu vực **Singapore (ap-southeast-1)** để làm phân vùng triển khai mặc định nhằm tối ưu hóa độ trễ kết nối đối với người dùng cuối tại thị trường Đông Nam Á và đảm bảo tính tương thích của tất cả các dịch vụ AWS được sử dụng trong sơ đồ.