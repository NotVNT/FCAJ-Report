---
title: "Event 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---



# Bài thu hoạch Event 2

### Mục Đích Của Sự Kiện

- Định hướng tư duy làm sản phẩm thực tế.
- Chia sẻ kinh nghiệm thực chiến từ các cuộc thi Hackathon.
- Nâng cao nhận thức về an toàn thông tin và tuân thủ.
- Tối ưu hóa chi phí vận hành hệ thống hạ tầng và Cloud.
- Thúc đẩy khả năng tự tin giao tiếp và tư duy phản biện.
- Hiểu rõ bản chất công nghệ để thiết kế hệ thống bền vững.

### Danh Sách Diễn Giả

- **Anh Tinh Trương** - Platform Engineer tại GoTymex
- **Anh Phạm Nguyễn Hải Anh** - G-AsiaPacific VietNam, AWS Community Builder
- **Mr. Thịnh** - DevOps/Cloud Engineer tại FCAJ
- **UTMorpho** - Nhóm LotusHacks 2026
- **Anh Duc Dao** - Solution Architecture tại Kinetics
- **Chị Cát Vy** - Senior Business Systems Analyst của VPBank

### Nội Dung Nổi Bật

#### Xu Hướng Thị Trường Lao Động & Yêu Cầu Mới Cho Nhân Sự IT

- **Thực trạng giai đoạn giao thời**: Cuộc chạy đua đầu tư hạ tầng AI của các ông lớn toàn cầu tạo ra áp lực tối ưu chi phí ngắn hạn, khiến thị trường tuyển dụng (đặc biệt là vị trí Intern/Fresher) cạnh tranh khốc liệt hơn bao giờ hết (tỷ lệ chọi thực tế tại doanh nghiệp có thể lên tới 1 chọi 50).
- **Làn sóng công việc mới**: Sự bùng nổ của AI làm giảm chi phí tạo ra phần mềm, dẫn đến nhu cầu bảo trì, vận hành và mở rộng hệ thống tăng mạnh. Xuất hiện các vị trí mới như Platform Engineering và Off-Platform Engineering để gánh vác hệ thống cho doanh nghiệp.
- **3 món vũ khí bắt buộc phải trang bị**:
    - **Nền tảng kỹ thuật vững chắc**: Bằng đại học vẫn là điều kiện cần (bộ lọc hồ sơ) của các tổ chức lớn.
    - **Kiến thức nghiệp vụ thực tế (Domain/Case study)**: Phải hiểu rõ mô hình hoạt động của ngành mình nhắm tới (ví dụ: Tài chính - Ngân hàng).
    - **Sản phẩm thực tế (Product Mindset)**: Thay vì chỉ có các bài tập demo, ứng viên phải sở hữu sản phẩm thực chứng để thuyết phục nhà tuyển dụng.

#### Kỹ Thuật Làm Chủ Ngữ Cảnh Trong Giao Tiếp Với AI

- **Vấn nạn "Internet Buller"**: Thói quen kéo mọi prompt, plugin, rule mẫu trên mạng về dùng chung trong một phiên chat làm AI bị loãng ngữ cảnh, đổi context liên tục dẫn đến "ngơ" và sinh code lỗi.
- **Xây dựng Context đúng và đủ**: Khi prompt AI, cần cung cấp rõ ràng: Mục tiêu (Goal), Vai trò/Cấp độ của người hỏi (Role/Persona), Format mong muốn, và đặc biệt là chỉ đưa vào các tài liệu/quy tắc mang tính đặc thù riêng của dự án/doanh nghiệp (kiến thức chung AI đã có sẵn).
- **Bản chất của Temperature = 0**: Khi hạ temperature về 0, LLM sẽ chuyển sang cơ chế Greedy Decoding (Argmax) - luôn chọn từ có xác suất cao nhất. Tuy nhiên, do kỹ thuật làm tròn số thập phân của GPU và cơ chế gộp prompt để tối ưu chi phí của các nhà cung cấp API, kết quả trả về giữa các lần chạy vẫn có thể bị biến thiên (Randomness).
- **Chiến lược giảm thiểu (Mitigation Strategy)**: Để hệ thống chạy Production ổn định, cần bọc các service downstream để xử lý lỗi format, cân nhắc tự host model cục bộ (Local) để kiểm soát tuyệt đối, hoặc dùng cơ chế chạy nhiều Agent song song để bầu chọn kết quả đồng thuận nhất.

#### Trải Nghiệm Thực Tế Phát Triển Sản Phẩm AI (Hackathon Case Study)

- **Dự án "UTMorpho" (Winner Hackathon)**: Minh họa thực tế quá trình xây dựng một ứng dụng AI Editor hỗ trợ sinh giao diện (UI) và cho phép chỉnh sửa kéo-thả trực tiếp trên UI đó từ bản vẽ nháp hoặc hình ảnh trong vòng 36 tiếng.
- **Kiến trúc Multi-Agent phối hợp**: Dự án sử dụng cấu trúc liên tầng gồm 3 Agent chuyên biệt:
    - **Agent 1 (Vision Agent)**: Đọc và phân tích hình ảnh đầu vào sang file JSON.
    - **Agent 2 (Layout Agent)**: Nhận file JSON để tính toán kích thước, layout và CSS.
    - **Agent 3 (Design Agent)**: Nhận thông tin để sinh mã code HTML/CSS hoàn chỉnh.
- **Bài học xương máu từ thực tế**:
    - Tránh bẫy nhiều tính năng (Overthinking/Overfeature): Cần cắt bỏ những thứ rườm rà, chỉ tập trung tối ưu cho tính năng cốt lõi (Core Feature) để kịp tiến độ.
    - Giải quyết bài toán của chính mình: Ý tưởng tốt nhất không cần vĩ mô, mà là ý tưởng giải quyết được nỗi đau (Pain point) hàng ngày của chính team phát triển.

#### Công Nghệ Trợ Lý Agent & Ứng Dụng Phân Tích Dữ Liệu

- **Sự tiến hóa từ Chatbot lên Agent**: Khác với Chatbot truyền thống chỉ biết trả lời text, AI Agent là bộ não LLM được gắn thêm "cánh tay nối dài" là các Action/Function (thông qua giao thức như MCP) để có thể trực tiếp hành động: đặt lịch, tạo dashboard, gửi email...
- **Ứng dụng Amazon Q Business / QuickSight (Demo)**: Người dùng nghiệp vụ (Manager, CEO) không cần kỹ năng kỹ thuật chỉ cần upload file Excel dữ liệu thô vào khung chat, AI Agent sẽ tự động phân tích và trực tiếp dựng lên các bảng biểu phân tích (Dashboard) trực quan bằng tiếng Việt.
- **Tự động hóa cuộc họp**: Agent có khả năng tự động chuyển âm thanh cuộc họp thành văn bản (Transcribe), tóm tắt các quyết định và tự động phân phối việc (Next steps) đến email của từng thành viên qua Microsoft Teams hoặc Outlook.

#### Cơ Chế Giá Mới & Nền Tảng Bảo Mật Của CloudFront CDN

- **Flat-rate Pricing**: AWS ra mắt các gói CDN cố định (Free, Pro, Business, Premium) thay vì Pay-as-you-go truyền thống. Giải quyết triệt để nỗi lo "Bill Spike" khi hệ thống bị tấn công DDoS hoặc tăng lưu lượng truy cập bất thường. Nếu dùng quá hạn mức, hệ thống chỉ bị bóp băng thông chứ không tính thêm tiền.
- **Hạ tầng mạng nội bộ cực tốc (AWS Backbone)**: Với gần 700 điểm hiện diện (PoP) cắm trực tiếp vào các nhà mạng lớn, lưu lượng từ CDN về server gốc (Origin) được truyền tải qua cáp quang nội bộ của AWS, giúp bypass internet công cộng và chống nghẽn mạch khi "cá mập cắn cáp".
- **Bảo mật nâng cao tại vùng biên (Edge)**:
    - Chặn đứng các cuộc tấn công volumetric attack (DDoS) ngay tại server Edge quốc gia của Botnet, không để traffic độc hại chạm tới server gốc.
    - Ứng dụng thư viện mã hóa S2N chống máy tính lượng tử giải mã và tính năng Mutual TLS (mTLS) yêu cầu xác thực chứng chỉ từ cả 2 phía (Client & Server), ứng dụng mạnh cho ngành Tài chính.
- **Tính năng VPC Origin**: Tạo đường hầm ẩn hoàn toàn Server gốc nằm trong Private Subnet khỏi Internet, chỉ cho phép CloudFront đi vào trực tiếp.

#### Kiến Trúc Multi-Agent Hệ Doanh Nghiệp (Enterprise-Grade)

- **Bài toán thực tế**: Thiết kế hệ thống Multi-Agent để đánh giá điểm tín dụng cho các doanh nghiệp Startup tại Việt Nam - đối tượng thường bị các mô hình ngân hàng truyền thống từ chối vì thiếu báo cáo tài chính 3 năm hoặc tài sản thế chấp.
- **Phân rã chuyên môn trong Enterprise**: Hệ thống được thiết kế như một Hội đồng tín dụng (Credit Committee) gồm một Host (Orchestrator) điều phối và các Sub-Agent chuyên trách: **Financial Analyst** (xử lý dòng tiền), **Market Analyst** (quét thị phần TAM/SAM/SOM), **Team Evaluator** (quét uy tín founder trên LinkedIn/Facebook) và **Risk Assessor** (đánh giá rủi ro).
- **Rào cản Security & Compliance**: Trong doanh nghiệp lớn, an ninh bảo mật luôn đi trước công nghệ. Không được tự ý cắm bừa bãi công cụ AI vì rủi ro rò rỉ dữ liệu (MCP attack vector). Mọi quy trình AI sinh kết quả đều bắt buộc phải có con người kiểm duyệt (Human-in-the-loop) và lưu vết (Audit trail), vì trước pháp luật, con người là bên chịu trách nhiệm tối cao chứ không phải AI.

#### Một số hình ảnh khi tham gia sự kiện
<div style="display: flex; gap: 20px; flex-wrap: wrap;">
    <img src="/images/4-EventParticipated/4.2-Event2/event1.jpg" alt="Ảnh event 1" width="400" height="400" style="object-fit: cover; border-radius: 8px;">
    <img src="/images/4-EventParticipated/4.2-Event2/event2.jpg" alt="Ảnh event 2" width="400" height="400" style="object-fit: cover; border-radius: 8px;">
    <img src="/images/4-EventParticipated/4.2-Event2/event3.jpg" alt="Ảnh event 3" width="400" height="400" style="object-fit: cover; border-radius: 8px;">
    <img src="/images/4-EventParticipated/4.2-Event2/event4.jpg" alt="Ảnh event 4" width="400" height="400" style="object-fit: cover; border-radius: 8px;">
    <img src="/images/4-EventParticipated/4.2-Event2/event5.jpg" alt="Ảnh event 5" width="400" height="400" style="object-fit: cover; border-radius: 8px;">
</div>