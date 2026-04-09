# Xanh SM - AI Customer Support Agent Demo

Ứng dụng demo chatbot hỗ trợ khách hàng cho Xanh SM với giao diện hiện đại và backend AI agent sử dụng LangGraph.

## 📁 Cấu trúc thư mục

```
xanhsm-demo/
├── backend/
│   ├── app.py              # Flask API server
│   ├── requirements.txt    # Python dependencies
│   └── .env               # Environment variables (tạo file này)
├── xanhsm-app.html        # Frontend application
└── README.md              # Hướng dẫn này
```

## 🚀 Cài đặt Backend

### 1. Cài đặt Python dependencies

```bash
cd backend
pip install -r requirements.txt
```

### 2. Tạo file .env

Tạo file `.env` trong thư mục `backend/` với nội dung:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

### 3. Tích hợp với agent hiện tại của bạn

File `backend/app.py` hiện đang sử dụng mock tools. Để tích hợp với agent thực của bạn:

**Option 1: Copy toàn bộ agent code**
- Copy file `agent.py`, `tool.py`, và `system_promt.txt` của bạn vào thư mục `backend/`
- Uncomment các import trong `app.py`:
  ```python
  from tool import create_ticket, lookup_trip
  ```
- Comment các mock functions

**Option 2: Sử dụng agent như một module**
- Đảm bảo agent của bạn export function `build_graph()`
- Import và sử dụng trong `app.py`

### 4. Chạy Backend Server

```bash
python app.py
```

Server sẽ chạy tại: `http://localhost:5000`

## 🎨 Sử dụng Frontend

### Cách 1: Mở trực tiếp file HTML

```bash
# Mở file trong browser
open xanhsm-app.html  # macOS
start xanhsm-app.html  # Windows
xdg-open xanhsm-app.html  # Linux
```

### Cách 2: Sử dụng Live Server (khuyến nghị)

Nếu bạn dùng VS Code:
1. Cài extension "Live Server"
2. Right-click vào `xanhsm-app.html` → "Open with Live Server"

Hoặc sử dụng Python:
```bash
python -m http.server 8000
# Mở http://localhost:8000/xanhsm-app.html
```

## ✨ Tính năng

### Scene 1 - Màn hình chính
- Hiển thị các dịch vụ của Xanh SM
- Banner khuyến mãi
- Icon robot floating ở góc phải dưới

### Scene 2 - Chat Interface
- Giao diện chat hiện đại
- Quick actions cho các câu hỏi thường gặp
- Tích hợp với AI agent backend
- Typing indicator khi AI đang xử lý
- Auto-scroll to bottom

## 🔧 Tùy chỉnh

### Thay đổi API URL

Trong file `xanhsm-app.html`, tìm dòng:

```javascript
const API_URL = 'http://localhost:5000/api/chat';
```

Thay đổi URL nếu backend chạy ở port khác hoặc deploy lên server.

### Tùy chỉnh màu sắc

Các biến CSS trong `:root`:
```css
--xanh-primary: #00CED1;
--xanh-dark: #008B8D;
--xanh-light: #7FFFD4;
```

### Tùy chỉnh system prompt

Trong `backend/app.py`, chỉnh sửa biến `system_prompt`:
```python
system_prompt = """Bạn là trợ lý ảo Xanh của Xanh SM..."""
```

## 🛠️ Troubleshooting

### CORS Error
Nếu gặp lỗi CORS, đảm bảo backend đã cài `flask-cors`:
```bash
pip install flask-cors
```

### Connection Refused
- Kiểm tra backend đã chạy chưa (`python app.py`)
- Kiểm tra port 5000 có bị chiếm không
- Thử port khác: `app.run(port=5001)`

### API Key Error
- Đảm bảo đã tạo file `.env` với `OPENAI_API_KEY`
- Kiểm tra API key còn credits

## 📱 Responsive Design

Giao diện đã được tối ưu cho:
- Desktop (>1024px)
- Tablet (768px - 1024px)
- Mobile (375px - 768px)

## 🎯 Next Steps

1. **Kết nối database** để lưu lịch sử chat
2. **Authentication** để phân biệt người dùng
3. **Analytics** để theo dõi metrics (accept rate, resolution rate)
4. **Deploy** lên production server
5. **Add more tools**: Tra cứu chuyến đi, hoàn tiền, v.v.

## 📄 License

MIT License - tự do sử dụng cho dự án của bạn.

## 🙋 Support

Nếu có vấn đề, hãy kiểm tra:
1. Console log trong browser (F12)
2. Terminal log của Flask server
3. File `XanhSM.log` nếu có

---

**Made with ❤️ for Xanh SM Hackathon**
