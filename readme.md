# MernorCloud (Zpiltk)

<div align="center">

**Hệ thống Cloud Storage lưu trữ tệp không giới hạn qua Telegram được tối ưu bằng Golang.**

</div>

---

## ✨ Tính năng nổi bật

* 📁 **Lưu trữ không giới hạn**: Lưu file trực tiếp trên Telegram không giới hạn dung lượng (hỗ trợ tự động chia nhỏ file lớn).
* 🎬 **Phát trực tiếp Media & Phụ đề**: Stream video và nhạc trực tiếp trên web với trình phát chuyên nghiệp, hỗ trợ phụ đề rời (`.srt`, `.vtt`, `.ass`).
* 📚 **Đọc tài liệu & Truyện online**: Tích hợp sẵn trình đọc sách điện tử **EPUB**, truyện tranh **CBZ** và tài liệu **PDF**.
* 🔗 **Chia sẻ linh hoạt**: Hỗ trợ link chia sẻ công khai, link tải trực tiếp (Direct Link) cho cả tệp và **thư mục**, có mật khẩu bảo vệ.
* ⚡ **Nén & Tải thư mục trực tiếp**: Hỗ trợ ZIP streaming tức thì từ server mà không tốn dung lượng ổ đĩa.
* 🗂️ **Quản lý trực quan**: File Browser với chế độ xem **Lưới (Grid)** và **Danh sách (List)**, tích hợp thùng rác khôi phục file.
* 📂 **Hỗ trợ WebDAV & S3 API**: Gắn thành ổ đĩa mạng trên máy tính hoặc kết nối với Rclone, Cyberduck, Infuse...
* 📥 **Tải URL, Video & Torrent**: Tích hợp `yt-dlp` và `aria2c` để tải video từ link và torrent trực tiếp về Telegram trong nền.
* 👥 **Đa người dùng**: Hỗ trợ tạo tài khoản con với không gian lưu trữ riêng biệt.
* 🤖 **Multi-Bot (Bot Pool)**: Phân phối tải trên nhiều Bot Telegram để tăng tốc độ upload/download tối đa.
* 🔐 **Bảo mật Passkey & Mã hóa**: Hỗ trợ đăng nhập sinh trắc học (Fingerprint, FaceID) và mã hóa dữ liệu nhạy cảm AES-256-GCM.
* 🗄️ **Hỗ trợ đa Database**: Hỗ trợ **SQLite**, **PostgreSQL** và **MySQL**.

---

## 🚀 Triển khai nhanh

### 1. Triển khai với Docker (Khuyên dùng)

```bash
docker run -d \
    --name mernorcloud \
    --restart unless-stopped \
    -p 8091:8091 \
    -v "$(pwd)/data:/app/data" \
    --env-file .env \
    -e DATABASE_PATH=/app/data/database.db \
    -e THUMBS_DIR=/app/data/thumbs \
    -e TEMP_DIR=/app/data/temp \
    ghcr.io/kanpief/mernorcloud
```

Hoặc sử dụng `docker-compose.yml`:
```bash
docker compose up -d
```

### 2. Triển khai trên Render / Cloud PaaS
1. Tạo Web Service chọn runtime **Docker**.
2. Thêm các biến môi trường:
   - `TELECLOUD_MASTER_KEY`: *[Khóa mã hóa 64 ký tự hex]*
   - `DATABASE_DRIVER`: `postgres`
   - `DATABASE_DSN`: *[URL kết nối PostgreSQL]*
   - `TEMP_DIR`: `/tmp`
3. Deploy và truy cập giao diện để hoàn tất cài đặt ban đầu.

---

## ⚙️ Cấu hình cơ bản

Sao chép file mẫu `env.example` thành `.env` để tuỳ chỉnh:

```env
# Master key mã hóa (32-byte hex)
TELECLOUD_MASTER_KEY=

# Cổng khởi chạy server (mặc định 8091)
PORT=8091

# Luồng tải lên song song
TG_UPLOAD_THREADS=2

# Cấu hình Database (sqlite / postgres / mysql)
DATABASE_DRIVER=sqlite
DATABASE_PATH=data/database.db
```

---

## 📜 Giấy phép

Phát hành dưới giấy phép [GNU Affero General Public License v3.0 (AGPL-3.0)](https://www.gnu.org/licenses/agpl-3.0.html).
