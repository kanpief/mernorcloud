# 🔌 API Documentation / Tài liệu API

MernorCloud (Zpiltk Edition) cung cấp hệ thống RESTful API mạnh mẽ để tích hợp vào các script tự động, ứng dụng bên thứ ba hoặc CI/CD pipeline.  
Comprehensive RESTful API documentation for MernorCloud (Zpiltk Edition).

---

## 🇻🇳 Tiếng Việt

### 1. Xác thực & Base URL
- **Base URL**: `http://<your-domain>/api/upload-api`
- **Xác thực**: Gửi Bearer Token qua HTTP Header:
  - Header: `Authorization: Bearer <YOUR_API_KEY>`
  - Lấy API Key tại: **Cài đặt -> Upload API** trên giao diện Web Admin.

---

### 2. Danh sách Endpoints

#### A. Tải tệp lên (Local Upload)
Tải tệp tin trực tiếp lên kho lưu trữ Telegram.
- **Endpoint**: `POST /upload`
- **Content-Type**: `multipart/form-data`
- **Tham số**:
  - `file`: (Bắt buộc) Tệp tin cần tải lên.
  - `path`: (Tùy chọn) Thư mục lưu trữ đích (Mặc định: `/`).
  - `share`: (Tùy chọn) Giá trị `public` để tự động tạo link chia sẻ sau khi tải xong.
  - `async`: (Tùy chọn) Giá trị `true` để xử lý tác vụ trong nền (trả về `task_id`).

#### B. Tải tệp từ URL từ xa (Remote Upload)
Tải tệp từ đường dẫn URL (Hỗ trợ Direct Link, YouTube, Facebook, TikTok...) về Telegram.
- **Endpoint**: `POST /remote`
- **Content-Type**: `application/json`
- **Tham số (JSON)**:
  - `url`: (Bắt buộc) Đường dẫn URL cần tải.
  - `path`: (Tùy chọn) Thư mục lưu trữ đích.
  - `async`: (Tùy chọn) Mặc định `true`.

#### C. Tạo liên kết chia sẻ (Create Share Link)
Tạo link chia sẻ cho tệp hoặc thư mục đã có.
- **Endpoint**: `POST /share`
- **Content-Type**: `application/json`
- **Tham số (JSON)**:
  - `path`: (Bắt buộc) Đường dẫn tệp/thư mục cần chia sẻ.

#### D. Kiểm tra trạng thái tác vụ (Task Status)
- **Endpoint**: `GET /tasks/<TASK_ID>`

#### E. Hủy tác vụ đang chạy (Cancel Task)
- **Endpoint**: `DELETE /tasks/<TASK_ID>`

---

### 3. Ví dụ cURL

**Tải lên tệp:**
```bash
curl -X POST http://localhost:8091/api/upload-api/upload \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -F 'file=@/path/to/file.zip' \
  -F 'path=/'
```

**Tải từ URL từ xa (Remote URL):**
```bash
curl -X POST http://localhost:8091/api/upload-api/remote \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"url": "https://example.com/video.mp4", "path": "/", "async": true}'
```

---

## 🇺🇸 English

### 1. Authentication & Base URL
- **Base URL**: `http://<your-domain>/api/upload-api`
- **Header**: `Authorization: Bearer <YOUR_API_KEY>`

### 2. Available Endpoints
- `POST /upload`: Upload local file to Telegram.
- `POST /remote`: Remote download from URL to Telegram.
- `POST /share`: Create share link for a path.
- `GET /tasks/<TASK_ID>`: Get asynchronous background task progress.
- `DELETE /tasks/<TASK_ID>`: Cancel a running task.
