# ⚙️ Configuration Guide / Hướng dẫn cấu hình

Thông tin chi tiết về các biến môi trường và thiết lập reverse proxy cho MernorCloud (Zpiltk Edition).  
Detailed guide on configuring MernorCloud (Zpiltk Edition) via environment variables and reverse proxies.

---

## 🇻🇳 Tiếng Việt

### 1. Tệp .env (Biến môi trường)

Sao chép tệp `env.example` thành `.env` trong thư mục chạy ứng dụng:

*   `API_ID` & `API_HASH`: Mặc định đã được tích hợp sẵn. Người dùng thông thường **không cần cấu hình**. Tùy chọn này chỉ dành cho nhà phát triển muốn dùng API riêng khi tự biên dịch.
*   `LOG_GROUP_ID`: (Tùy chọn) ID nhóm/kênh lưu file hoặc điền `me`. Nếu để trống, bạn có thể thiết lập qua giao diện Web Setup.
    *   **Cách lấy LOG_GROUP_ID**: Tạo nhóm Telegram mới, bật hiển thị lịch sử trong cài đặt nhóm, thêm bot `@get_all_telegram_id_bot` và gửi lệnh `/getid`. ID nhóm có dạng `-100xxxxxxxxxx`.
*   `PORT`: Cổng khởi chạy HTTP server (mặc định: `8091`).
*   `LISTEN_ADDR`: (Tùy chọn) Địa chỉ IP lắng nghe (mặc định: `0.0.0.0`). Có thể đổi thành `127.0.0.1` nếu đặt sau Cloudflare Tunnel, Nginx hoặc Reverse Proxy.
*   `TG_UPLOAD_THREADS`: Số luồng tải lên song song cho mỗi part (mặc định: `2`, tối đa khuyến nghị: `4`).
*   `TG_DOWNLOAD_PREFETCH`: Số chunk 1MB tải trước song song khi stream/download (mặc định: `4`, từ `2` đến `16`).
*   `DATABASE_DRIVER`: Loại cơ sở dữ liệu (`sqlite`, `mysql` hoặc `postgres`). Mặc định: `sqlite`.
*   `DATABASE_PATH`: Đường dẫn tới tệp database SQLite (mặc định: `data/database.db`).
*   `DATABASE_DSN`: Chuỗi kết nối nếu dùng MySQL / PostgreSQL:
    *   MySQL: `user:pass@tcp(127.0.0.1:3306)/mernorcloud?parseTime=true&charset=utf8mb4`
    *   Postgres: `postgres://user:pass@127.0.0.1:5432/mernorcloud?sslmode=disable`
*   `TELECLOUD_MASTER_KEY`: Khóa 32-byte (64 hex) dùng để mã hóa session và settings. Nếu để trống, hệ thống sẽ tự sinh và lưu vào `master.key`.
*   `THUMBS_DIR`: Đường dẫn thư mục ảnh thu nhỏ (mặc định: `data/thumbs`).
*   `TEMP_DIR`: Đường dẫn thư mục file tạm (mặc định: `data/temp`).
*   `COOKIES_DIR`: Đường dẫn thư mục chứa cookie yt-dlp (mặc định: `data/cookies`).
*   `PROXY_URL`: (Tùy chọn) Proxy kết nối MTProto, hỗ trợ HTTP và SOCKS5 (VD: `socks5://127.0.0.1:1080`).
*   `FFMPEG_PATH`: Đường dẫn tới FFmpeg binary (đặt `disabled` để tắt tạo thumbnail).
*   `YTDLP_PATH`: Đường dẫn tới yt-dlp binary (đặt `disabled` để tắt tính năng tải URL).
*   `TORRENT_PATH`: Đường dẫn tới aria2c binary (đặt `disabled` để tắt tính năng tải Torrent).

---

### 2. Tinh chỉnh `TG_DOWNLOAD_PREFETCH`

Bộ đệm tải trước (*read-ahead prefetch*) tải song song các chunk 1MB tiếp theo để tăng tốc độ phát video và tải file:

| Tình huống | Giá trị khuyến nghị |
| :--- | :--- |
| Mặc định, phù hợp hầu hết nhu cầu | `4` |
| VPS RAM thấp (≤ 1GB) hoặc nhiều kết nối đồng thời | `2` |
| Khi gặp cảnh báo `FLOOD_WAIT` từ Telegram | `2` |
| Có Bot Pool lớn (5+ bot) và mạng tốc độ cao | `8` |

---

### 3. Cấu hình Nginx Reverse Proxy (Khuyên dùng)

Mẫu cấu hình Nginx tối ưu hỗ trợ streaming, WebSocket và S3 API:

```nginx
server {
    listen 80;
    server_name cloud.example.com;

    # Cho phép tải file kích thước lớn không giới hạn
    client_max_body_size 0;

    location / {
        proxy_pass http://127.0.0.1:8091;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # Hỗ trợ Range Requests cho streaming mượt mà
        proxy_set_header Range $http_range;
        proxy_set_header If-Range $http_if_range;

        proxy_request_buffering off;
        proxy_buffering off;
        proxy_read_timeout 3600s;
    }

    # Hỗ trợ WebSocket
    location /api/ws {
        proxy_pass http://127.0.0.1:8091/api/ws;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_read_timeout 3600s;
    }

    # Hỗ trợ S3 API
    location /s3 {
        proxy_pass http://127.0.0.1:8091;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_request_buffering off;
        proxy_buffering off;
        client_max_body_size 0;
    }
}
```

---

## 🇺🇸 English

### 1. Environment Variables (`.env`)

* `PORT`: Server listening port (default: `8091`).
* `LISTEN_ADDR`: Server listening address (default: `0.0.0.0`).
* `TG_UPLOAD_THREADS`: Upload concurrency per part (default: `2`).
* `TG_DOWNLOAD_PREFETCH`: Read-ahead chunk count (default: `4`, range: `2-16`).
* `DATABASE_DRIVER`: Database type (`sqlite`, `mysql`, `postgres`).
* `DATABASE_PATH`: SQLite database file path.
* `DATABASE_DSN`: Connection string for PostgreSQL / MySQL.
* `TELECLOUD_MASTER_KEY`: 32-byte master key for AES-256-GCM encryption.
* `PROXY_URL`: SOCKS5/HTTP MTProto proxy URL.
