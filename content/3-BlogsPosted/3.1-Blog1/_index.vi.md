---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Xây Dựng Ứng Dụng Yêu Cầu Nhiều Bộ Nhớ Dễ Dàng Hơn Với AWS Lambda Managed Instances

### AWS Lambda Managed Instances Là Gì?

Tính năng này cho phép bạn chạy các hàm AWS Lambda trên các phiên bản Amazon EC2 do bạn tự chọn (bao gồm dòng tối ưu hóa bộ nhớ hay Graviton4). Điểm đột phá là nó cung cấp lên đến **32 GB RAM** – cao gấp 3 lần giới hạn cũ của Lambda. Toàn bộ vòng đời hạ tầng (cung cấp, mở rộng, vá lỗi...) đều được AWS quản lý tự động.

### Điểm Nổi Bật & Lợi Ích Cốt Lõi

- **Đa luồng đồng thời (Multi-concurrent invocations)**: Một môi trường thực thi có thể xử lý nhiều yêu cầu cùng lúc, giúp tăng hiệu suất tối đa cho các ứng dụng nặng về I/O.
- **Mở rộng không độ trễ (Dynamic scaling)**: Hệ thống tự động mở rộng dựa trên mức sử dụng CPU mà không gặp phải tình trạng "cold start" (khởi động lạnh).
- **Linh hoạt chọn phần cứng**: Lập trình viên có thể tùy ý chọn dòng máy tính toán (C), đa dụng (M) hoặc tối ưu bộ nhớ (R) và điều chỉnh tỷ lệ RAM - CPU sao cho phù hợp nhất.
- **Tiết kiệm chi phí**: Nhờ sử dụng biểu giá EC2, doanh nghiệp có thể áp dụng Savings Plans để giảm tới **33%** chi phí so với mức giá Lambda tiêu chuẩn cho các khối lượng công việc dễ dự đoán.

### Các Trường Hợp Sử Dụng Lý Tưởng

Giải pháp này tỏa sáng ở các hệ thống đòi hỏi tải lượng lớn dữ liệu vào bộ nhớ:

1. **Phân tích trong bộ nhớ (In-Memory Analytics)**: Tải hàng Gigabyte dữ liệu để truy vấn với độ trễ chỉ tính bằng mili-giây.
2. **Chạy mô hình Machine Learning**: Giữ các mô hình AI trực tiếp trong RAM để suy luận nhanh chóng mà không tốn tiền duy trì một endpoint riêng (như Amazon SageMaker).
3. **Tìm kiếm ngữ nghĩa (Semantic Search)**: Duy trì các chỉ mục vector (vector indexes) ngay trong bộ nhớ để truy vấn ngôn ngữ tự nhiên mà không cần đến Vector Database bên ngoài.
4. **Tính toán khoa học & Xử lý đồ thị**: Tối ưu cho các thuật toán phức tạp cần quét qua toàn bộ tập dữ liệu lớn cùng lúc.

### Ví Dụ Thực Tế: AI-Powered Customer Analytics

Trong bài viết, AWS demo việc xây dựng một hệ thống phân tích khách hàng. Hệ thống này tải **1 triệu bản ghi** (định dạng Parquet từ S3) và mô hình tìm kiếm FastEmbed vào thẳng bộ nhớ khi khởi tạo hàm. Tổng dung lượng ngốn khoảng **14 GB RAM** (điều bất khả thi với Lambda truyền thống). Kết quả đạt được là một ứng dụng Serverless có thể phân tích xu hướng và tìm kiếm thông tin khách hàng trong thời gian thực (sub-second) mà đội ngũ IT không phải quản lý bất kỳ một máy chủ EC2 nào.

<div style="display: flex; gap: 20px; flex-wrap: wrap;">
    {{< rimg src="/images/3-BlogsPosted/3.1-Blog1/blog1_img.jpg" alt="Blog 1 image" width="400" style="border-radius: 8px;" >}}
</div>

### Kết Luận

Việc xây dựng ứng dụng cần RAM khủng không còn đồng nghĩa với việc phải từ bỏ mô hình Serverless. **AWS Lambda Managed Instances** là sự kết hợp hoàn hảo giữa sức mạnh phần cứng của Amazon EC2 và sự đơn giản, tự động của AWS Lambda. Đây là bước đệm tuyệt vời cho các dự án Data Analytics và AI/ML.

**Link bài viết gốc**: [Building memory-intensive apps with AWS Lambda Managed Instances](https://aws.amazon.com/blogs/compute/building-memory-intensive-apps-with-aws-lambda-managed-instances/)