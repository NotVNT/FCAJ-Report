---
title: "Tự đánh giá"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 6. </b> "
---



Tới thời điểm này thì em đã qua phần nền tảng và bắt đầu vào giai đoạn làm dự án thực tế rồi. Nhân dịp này em muốn tự nhìn lại xem mấy tháng vừa rồi em tiến được tới đâu, cái gì ổn rồi và cái gì vẫn còn yếu.

Nói thật thì hồi mới vào em khá bỡ ngỡ. Công việc hàng tuần chủ yếu là làm lab trên AWS, đọc tài liệu, viết worklog rồi dịch blog. Nghe thì đơn giản nhưng tuần nào cũng có cái mới nên cũng phải cố gắng theo kịp. Được cái là càng làm thì em càng bớt phải nhìn hướng dẫn từng bước, tự xử lý được nhiều hơn. Nhưng em cũng tự biết là hiện tại em chỉ mới vững phần cơ bản thôi, còn nhiều thứ phải học nữa.

### Những gì em thấy em tiến bộ

- **Quen tay hơn với các dịch vụ AWS**: Hồi đầu em chỉ biết tên, giờ thì đã thực sự động vào IAM, VPC, EC2, RDS, S3, CloudWatch, Auto Scaling, Route 53, CloudFront, DynamoDB, Lambda, API Gateway, CloudFormation. Không phải là giỏi gì, nhưng ít nhất em có thể tự làm lại lab, hiểu tại sao phải cấu hình như vậy và tự sửa được một số lỗi cơ bản.
- **Bớt hoảng khi gặp lỗi**: Trước đây cứ lỗi là em làm lại từ đầu hoặc hỏi ngay. Giờ thì em biết nên check Security Group, Route Table, IAM Policy hay xem log CloudWatch trước. Chưa phải lúc nào cũng tìm ra nguyên nhân, nhưng ít nhất có hướng đi chứ không còn loay hoay như trước.
- **Biết cách tự học hơn**: Cái lộ trình theo tuần nó ép em phải đi đúng tiến độ, nên dần dần em quen với việc đọc trước, làm lab, rồi ghi lại cái nào hiểu cái nào chưa. Trước thì cứ làm cho xong, giờ em hay dừng lại hỏi "tại sao phải config vậy" nhiều hơn.
- **Biết lo chuyện chi phí trên cloud**: Cái này hồi đầu em không để ý lắm. Nhưng sau vài lần thấy bill chạy lên vì quên tắt dịch vụ là em sợ luôn. Giờ em xong lab là xóa tài nguyên liền, rồi hay vào kiểm tra billing xem có gì còn chạy không.
- **Viết lách đỡ hơn trước**: Nhờ viết worklog và dịch blog hàng tuần nên cách diễn đạt của em cải thiện được kha khá. Vẫn chưa gọn lắm nhưng so với mấy tuần đầu thì đỡ lan man hơn nhiều rồi.

### Những gì em cần cải thiện

- **Chưa biết tự thiết kế kiến trúc**: Nếu có sẵn sơ đồ hoặc lab hướng dẫn thì em làm được. Nhưng nếu ai đó đưa cho em một yêu cầu kiểu "làm hệ thống A cho khách hàng B" rồi bảo em tự đề xuất kiến trúc thì em vẫn chưa biết bắt đầu từ đâu.
- **IaC còn yếu**: Em biết CloudFormation là gì, đã chạy thử vài template, nhưng phần lớn vẫn đang click tay trên Console. Em biết kiểu làm này không bài bản, nên cần phải tập dùng infrastructure as code nhiều hơn.
- **Networking nâng cao thì vẫn mù mờ**: VPC cơ bản thì ok, nhưng mấy cái như hybrid networking, Transit Gateway, hay thiết kế mạng phức tạp nhiều tầng thì em đọc vẫn thấy khó hiểu. Mảng này em cần đầu tư thêm nhiều.
- **Chưa có kinh nghiệm ghép hệ thống hoàn chỉnh**: Em toàn làm từng lab rời rạc, chưa bao giờ tự ghép từ đầu tới cuối thành một hệ thống có đầy đủ monitoring, testing, deployment. Cái này chắc phải tới phần dự án mới được trải nghiệm.
- **Hay bị động khi nhiều việc cùng lúc**: Mấy tuần bài trường nhiều mà lab cũng dày thì em hay bị cuống, không biết ưu tiên cái nào trước. Kỹ năng quản lý thời gian em vẫn cần cải thiện thêm.

### Nhìn chung

Nếu tự chấm thì em nghĩ em đã đi từ mức "biết tên dịch vụ" lên mức "tự làm được, tự kiểm tra được và biết cách học tiếp". Chưa phải giỏi, nhưng so với lúc mới vào thì khác nhiều.

Em biết em chưa sẵn sàng cho mấy bài toán kiến trúc hay triển khai phức tạp. Hiện tại em đang ở giai đoạn xây nền, cố lấp mấy khoảng trống về IaC, CI/CD, thiết kế hệ thống. Em hy vọng phần còn lại của chương trình sẽ giúp em biến mấy kiến thức rời rạc thành cái gì đó thực tế hơn.