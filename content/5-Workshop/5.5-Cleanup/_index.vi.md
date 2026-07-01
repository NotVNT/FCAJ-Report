---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

Sau khi kết thúc phiên thực hành, tiến hành dọn dẹp các tài nguyên hạ tầng thử nghiệm để tránh phát sinh chi phí duy trì trên tài khoản AWS:

1. Xóa toàn bộ các tệp tin ảnh kiểm thử đã tải lên S3 bucket **botdevgroup-documents** để tránh phí lưu trữ dung lượng hàng tháng.
2. Thực hiện xóa **Interface VPC Endpoint** vpce-s3-interface để giải phóng Network Interface và dừng tính phí duy trì hàng giờ của dịch vụ AWS PrivateLink.
3. Hủy liên kết (Detach) **Gateway VPC Endpoint** vpce-s3-gateway khỏi Route Table của Private Subnets để trả cấu hình định tuyến ban đầu của mạng VPC.
4. Xóa các nhóm bảo mật Security Group và các bản ghi DNS thử nghiệm trên Route 53 Resolver.
5. Chạy lệnh dọn dẹp Docker cache (`docker system prune -af`) trên máy chủ EC2 để giải phóng dung lượng ổ đĩa EBS.