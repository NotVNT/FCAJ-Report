---
title: "Các bài blogs đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---



Tại đây sẽ là phần liệt kê, giới thiệu các blogs mà nhóm chúng em đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj).

###  [Blog 1 - Xây Dựng Ứng Dụng Yêu Cầu Nhiều Bộ Nhớ Dễ Dàng Hơn Với AWS Lambda Managed Instances](3.1-Blog1/)
Các ứng dụng hiện đại ngày càng cần nhiều dung lượng bộ nhớ để xử lý dữ liệu lớn, phân tích phức tạp hoặc chạy các mô hình Machine Learning (ML). Để giải quyết bài toán này, AWS đã giới thiệu AWS Lambda Managed Instances – một giải pháp giúp vượt qua giới hạn bộ nhớ của Lambda tiêu chuẩn nhưng vẫn giữ trọn vẹn sự tiện lợi của kiến trúc Serverless (không máy chủ).

###  [Blog 2 - OpenSearch Serverless Thế Hệ Mới: Vector Search Co Giãn Về 0 Cho Ứng Dụng AI Agent](3.2-Blog2/)
Các ứng dụng AI agent có một đặc điểm rất riêng về tải: một agent có thể bắn ra hàng trăm truy vấn vector trong lúc suy luận một tác vụ, rồi im lặng hàng giờ. Với hạ tầng tìm kiếm truyền thống, bạn vẫn phải trả tiền cho phần năng lực không dùng tới trong những khoảng rảnh đó. Ngày 28/05/2026, AWS công bố thế hệ mới của Amazon OpenSearch Serverless (gọi là NextGen) – một search và vector engine được thiết kế lại từ đầu để phục vụ đúng kiểu workload bất định này.

###  [Blog 3 - Xây Dựng Workflow Nhiều Bước Đáng Tin Cậy Với AWS Lambda Durable Functions](3.3-Blog3/)
Các ứng dụng hiện đại thường phải xử lý những quy trình gồm nhiều bước nối tiếp nhau – ví dụ xử lý đơn hàng, onboarding người dùng, hoặc điều phối các workflow AI gọi nhiều lần đến mô hình ngôn ngữ (LLM) và công cụ bên ngoài. Trước đây, để làm việc này trên AWS Lambda, lập trình viên phải ghép nối thêm Step Functions, SQS, DynamoDB để lưu trạng thái, dẫn đến hạ tầng phức tạp. Tại re:Invent 2025, AWS giới thiệu AWS Lambda Durable Functions – cho phép viết toàn bộ workflow dưới dạng mã tuần tự ngay trong một hàm Lambda duy nhất, mà vẫn giữ được khả năng chịu lỗi và tạm dừng dài hạn.