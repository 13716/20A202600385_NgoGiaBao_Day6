# Individual reflection — Ngô Gia Bảo (20A202600385)

## 1. Role
Fullstack Developer + AI Integration. Phụ trách xây dựng backend (Flask/LangGraph), frontend (navigation, chat UI) và prompt engineering cho Xanh SM AI Agent.

## 2. Đóng góp cụ thể
- Thiết kế hệ thống AI Agent với LangGraph, tích hợp `MemorySaver` để duy trì ngữ cảnh trò chuyện, giúp agent có khả năng lưu trữ thông tin qua nhiều lượt tương tác.
- Tích hợp công cụ (tool calling) `create_ticket` để tự động tạo ticket hỗ trợ dựa trên việc hỏi và xác nhận thông tin từ người dùng.
- Xây dựng cơ chế điều hướng thông minh (intent/keyword-based navigation) giúp backend kích hoạt chuyển đổi mượt mà giữa các màn hình (Map, Food, Delivery, Voucher) dựa trên yêu cầu từ người dùng.
- Hoàn thiện UI/UX Frontend: full-screen app-like navigation, floating chat icon bám sát mọi màn hình, và cơ chế tự động hiển thị form đánh giá (feedback) sau 5s ngừng tương tác.

## 3. SPEC mạnh/yếu
- **Mạnh nhất**: Trải nghiệm người dùng (UX) — Flow điều hướng liền mạch, floating widget giúp user có thể chat ở bất cứ đâu. Khả năng AI Agent nhận diện intent và vừa trả lời vừa điều khiển UI (chuyển scene) chạy rất ổn định trên tổng thể kiến trúc hệ thống.
- **Yếu nhất**: Cơ chế feedback theo thời gian (Inactivity-based feedback) — Việc pop-up đánh giá hiện lên sau 5s không thao tác có thể làm gián đoạn nếu user chỉ đang dừng lại để đọc text dài của AI. Có thể gây ra trải nghiệm hơi gượng ép.

## 4. Đóng góp khác
- Thiết kế prompt đặc tả cho Agent để phân vùng chính xác khi nào chỉ cung cấp thông tin, khi nào cần chuyển cảnh UI, và khi nào cần gọi tool `create_ticket`.
- Fix lỗi đồng bộ state giữa backend trả về (scene navigation) và trạng thái hiển thị của frontend.
- Setup cấu trúc mã nguồn tích hợp (Flask tĩnh và API) gọn nhẹ cho mục tiêu demo nhanh.

## 5. Điều học được
Trước hackathon, tôi nghĩ làm AI chat chỉ là truyền text vào API LLM và in ra. Sau khi làm Xanh SM AI Agent, tôi mới hiểu phần phức tạp thực sự là kết nối AI vào hệ thống Stateful (giao diện, cơ sở dữ liệu nội bộ). Khả năng ra quyết định (Routing/Tool Calling) của AI quan trọng hơn nhiều so với khả năng sinh chữ tự nhiên. Quyết định khi nào trigger `create_ticket` cần độ chính xác cao để không làm phiền hệ thống CSKH.

## 6. Nếu làm lại
Sẽ cải thiện cơ chế hiển thị Feedback. Thay vì dùng rules cứng (5s timeout), tôi sẽ đẩy logic đánh giá "End of conversation" cho AI (Agent tự nhận diện cuộc hội thoại đã giải quyết xong vấn đề) để trigger màn hình đánh giá, giúp trải nghiệm tự nhiên hơn.
Ngoài ra, tôi sẽ dành thêm thời gian test kỹ hơn các failure modes của LangGraph khi người dùng cung cấp thông tin `create_ticket` bị thiếu nửa chừng rồi đánh trống lảng.

## 7. AI giúp gì / AI sai gì
- **Giúp:** AI (Claude/Gemini) hỗ trợ rất đắc lực để học siêu nhanh luồng làm việc của LangGraph (vốn tài liệu khá phức tạp), đặc biệt là setup `MemorySaver`. Generator các đoạn CSS transition mượt mà cho các màn hình frontend (glassmorphism, animation) cũng giúp tiết kiệm rất nhiều giờ code tay.
- **Sai/mislead:** AI từng suggest dùng Redux/Context API quá phức tạp chỉ để quản lý trạng thái mở popup chat ở frontend. Nó làm mất thời gian debug ban đầu. Bài học: AI hay có xu hướng over-engineering (gợi ý kiến trúc to lớn, phức tạp) và mình phải biết chặn lại để giữ scope vừa đủ cho một dự án hackathon.
