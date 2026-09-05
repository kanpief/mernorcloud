# MernorCloud (Zpiltk Edition)

<div align="center">

**Hệ thống Cloud Storage lưu trữ không giới hạn qua Telegram — Phiên bản tối ưu & tùy biến riêng bởi Zpiltk.**

[![Go Version](https://img.shields.io/badge/Go-1.24+-00ADD8?style=flat&logo=go)](https://golang.org)
[![License: AGPL-3.0](https://img.shields.io/badge/License-AGPL--3.0-blue.svg)](https://www.gnu.org/licenses/agpl-3.0.html)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=flat&logo=docker)](https://www.docker.com/)
[![WebDAV](https://img.shields.io/badge/Protocol-WebDAV%20%7C%20S3-orange.svg)](#-tính-năng-nổi-bật)
[![Telegram](https://img.shields.io/badge/Storage-Telegram%20MTProto-2CA5E0?style=flat&logo=telegram)](https://telegram.org)

</div>

---

## 📖 Giới thiệu

**MernorCloud (Zpiltk Edition)** là giải pháp lưu trữ đám mây cá nhân thế hệ mới, biến tài khoản Telegram thành một ổ đĩa đám mây không giới hạn dung lượng với tốc độ vượt trội. 

Dự án được **Zpiltk** xây dựng, tùy biến và tối ưu hóa sâu:
- **Độc lập & Tự chủ**: Tách biệt hoàn toàn thành phiên bản tùy biến riêng biệt, nâng cao tính bảo mật và quyền riêng tư.
- **Tối ưu hóa hiệu năng**: Bộ đệm song song (*prefetch chunks*), Bot Pool thông minh phân phối tải, nén và streaming ZIP theo thời gian thực không tốn ổ cứng server.
- **Tự quản lý Cookie yt-dlp**: Cho phép người dùng tự tải lên và gỡ bỏ Cookie YouTube/mạng xã hội riêng biệt cho từng tài khoản mà không phụ thuộc vào cookie dùng chung.
- **Hỗ trợ giao thức mở**: Tích hợp toàn diện chuẩn WebDAV và S3 API để gắn ổ đĩa trên Windows, macOS, Linux, hoặc đồng bộ với Rclone, Cyberduck, Infuse.

---

## ✨ Tính năng nổi bật

### 🚀 Lưu trữ & Băng thông
* 📁 **Lưu trữ không giới hạn**: Tận dụng hạ tầng Telegram để lưu trữ tệp không giới hạn dung lượng. Tự động chia nhỏ (chunking) file lớn thành các part an toàn.
* 🤖 **Multi-Bot (Bot Pool)**: Kết nối nhiều Bot Telegram chạy song song để tối đa hóa tốc độ tải lên và tải xuống, loại bỏ giới hạn băng thông đơn luồng.
* ⚡ **Nén & Tải thư mục tức thì (ZIP Streaming)**: Tải toàn bộ thư mục dưới dạng file `.zip` theo cơ chế stream trực tiếp từ Telegram về client mà không tốn dung lượng ổ đĩa máy chủ.

### 🎬 Giải trí & Đọc tài liệu
* 🎥 **Trình phát Media chuyên nghiệp**: Phát trực tiếp video và nhạc chất lượng cao trên trình duyệt, hỗ trợ phụ đề rời (`.srt`, `.vtt`, `.ass`) và ghi nhớ vị trí phát.
* 📖 **Trình đọc sách & truyện online**: Tích hợp sẵn trình đọc sách điện tử **EPUB**, đọc truyện tranh **CBZ** và xem tài liệu **PDF** mượt mà.

### 🌐 Kết nối & Tích hợp
* 📂 **WebDAV & S3-Compatible API**: Gắn MernorCloud thành ổ đĩa mạng trên máy tính hoặc kết nối với Infuse (Apple TV/iOS), Rclone, Cyberduck, Nextcloud.
* 📥 **Tải từ URL, Video & Torrent**: Tích hợp `yt-dlp` và `aria2c` để tải video YouTube/TikTok/Facebook hoặc tải torrent trực tiếp về Telegram chạy ngầm.
* 🍪 **Quản lý Cookie linh hoạt**: Mỗi tài khoản có thể tự upload file cookie của riêng mình để tải video giới hạn độ tuổi / video riêng tư và gỡ bỏ bất kỳ lúc nào.

### 👥 Quản trị & Bảo mật
* 👥 **Hệ thống đa người dùng (Multi-User)**: Phân chia không gian lưu trữ và quản lý quyền tài khoản con độc lập.
* 🔐 **Đăng nhập Passkey & Sinh trắc học**: Hỗ trợ chuẩn WebAuthn (TouchID, FaceID, Windows Hello) bảo mật và tiện lợi.
* 🛡️ **Mã hóa AES-256-GCM**: Mã hóa phiên làm việc Telegram và các thông số nhạy cảm trong cơ sở dữ liệu.
* 🗄️ **Hỗ trợ đa Database**: Tùy chọn linh hoạt giữa **SQLite** (nhẹ nhàng, mặc định), **PostgreSQL** hoặc **MySQL**.

---

## 🚀 Triển khai nhanh

### 1. Triển khai bằng Docker (Khuyên dùng)

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
    ghcr.io/kanpief/mernorcloud:latest
```

Hoặc sử dụng `docker-compose.yml`:

```yaml
services:
  mernorcloud:
    image: ghcr.io/kanpief/mernorcloud:latest
    container_name: mernorcloud
    restart: unless-stopped
    ports:
      - "8091:8091"
    env_file:
      - .env
    volumes:
      - ./data:/app/data
```

Khởi chạy bằng lệnh:
```bash
docker compose up -d
```

---

### 2. Triển khai tự động trên Linux / VPS / Termux

Sử dụng script cài đặt tự động với menu quản lý trực quan:

```bash
# Sử dụng cURL
curl -fsSL https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-setup.sh -o auto-setup.sh && bash auto-setup.sh

# Hoặc sử dụng wget
wget -qO auto-setup.sh https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-setup.sh && bash auto-setup.sh
```

---

### 3. Triển khai trên Windows

1. Tải script [`auto-install.bat`](https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-install.bat).
2. Click chuột phải chọn **Run as Administrator**.
3. Menu sẽ tự động tải FFmpeg, cấu hình Cloudflare Tunnel và khởi động ứng dụng chạy ngầm.

---

### 4. Triển khai trên Render / PaaS Cloud

1. Tạo một **Web Service** chọn môi trường **Docker**.
2. Thiết lập các biến môi trường:
   - `TELECLOUD_MASTER_KEY`: *[Chuỗi 64 ký tự hex ngẫu nhiên]*
   - `DATABASE_DRIVER`: `postgres`
   - `DATABASE_DSN`: *[URL kết nối cơ sở dữ liệu PostgreSQL]*
   - `TEMP_DIR`: `/tmp`
3. Deploy và truy cập `http://<dia-chi-web>/setup` để hoàn tất thiết lập ban đầu.

---

## ⚙️ Cấu hình Biến môi trường (`.env`)

Sao chép `env.example` thành `.env` để tuỳ biến theo nhu cầu:

```env
# Master key mã hóa dữ liệu nhạy cảm (32-byte hex)
TELECLOUD_MASTER_KEY=

# Cổng khởi chạy HTTP server (mặc định: 8091)
PORT=8091

# Địa chỉ IP lắng nghe (mặc định: 0.0.0.0)
LISTEN_ADDR=0.0.0.0

# Luồng tải lên song song cho mỗi part (mặc định: 2)
TG_UPLOAD_THREADS=2

# Số chunk tải trước khi streaming/download (2 - 16, mặc định: 4)
TG_DOWNLOAD_PREFETCH=4

# Loại Database: sqlite | postgres | mysql
DATABASE_DRIVER=sqlite
DATABASE_PATH=data/database.db
```

---

## 📚 Tài liệu chi tiết

* 🛠️ [Hướng dẫn Cài đặt](docs/Installation.md)
* ⚙️ [Hướng dẫn Cấu hình chi tiết](docs/Configuration.md)
* 🐳 [Triển khai nâng cao với Docker](docs/Docker.md)
* 🔌 [Tài liệu REST API](docs/API.md)
* 🔐 [Chính sách & Kiến trúc Bảo mật](docs/Security.md)
* 💻 [Hướng dẫn Phát triển & Biên dịch mã nguồn](docs/Development.md)

---

## 📜 Giấy phép & Bản quyền

Dự án được phân phối dưới giấy phép [GNU Affero General Public License v3.0 (AGPL-3.0)](https://www.gnu.org/licenses/agpl-3.0.html).  
Tùy biến & phát triển bởi **Zpiltk**.
