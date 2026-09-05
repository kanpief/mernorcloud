# 🐳 Docker Deployment / Triển khai với Docker

Hướng dẫn triển khai MernorCloud (Zpiltk Edition) bằng Docker và Docker Compose. Image đã được tối ưu và tích hợp sẵn **FFmpeg** và **yt-dlp**.  
Comprehensive guide for deploying MernorCloud (Zpiltk Edition) with Docker and Docker Compose.

---

## 🇻🇳 Tiếng Việt

### 1. Triển khai nhanh bằng lệnh Docker Run

```bash
# Tạo thư mục dữ liệu
mkdir -p data && chmod 777 data

# Khởi chạy container
docker run -d \
    --name mernorcloud \
    --restart unless-stopped \
    -p 8091:8091 \
    -v "$(pwd)/data:/app/data" \
    --env-file .env \
    -e DATABASE_PATH=/app/data/database.db \
    -e THUMBS_DIR=/app/data/thumbs \
    -e TEMP_DIR=/app/data/temp \
    --user 65532:65532 \
    ghcr.io/kanpief/mernorcloud:latest
```

---

### 2. Triển khai bằng Docker Compose (Khuyên dùng)

1. Tải hoặc tạo tệp `docker-compose.yml`:
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
       user: "65532:65532"
       environment:
         - DATABASE_PATH=/app/data/database.db
         - THUMBS_DIR=/app/data/thumbs
         - TEMP_DIR=/app/data/temp
         - FFMPEG_PATH=/usr/bin/ffmpeg
         - YTDLP_PATH=/usr/local/bin/yt-dlp
         - TORRENT_PATH=/usr/bin/aria2c
       volumes:
         - ./data:/app/data
   ```

2. Tạo tệp `.env` cấu hình từ mẫu `env.example`.
3. Khởi động dịch vụ:
   ```bash
   docker compose up -d
   ```

#### Các lệnh quản trị hữu ích:
* **Xem nhật ký**: `docker compose logs -f`
* **Dừng dịch vụ**: `docker compose stop`
* **Cập nhật image**: `docker compose pull && docker compose up -d`
* **Xóa container**: `docker compose down`

---

## 🇺🇸 English

### 1. Single Container (Quick Start)

```bash
mkdir -p data && chmod 777 data

docker run -d \
    --name mernorcloud \
    --restart unless-stopped \
    -p 8091:8091 \
    -v "$(pwd)/data:/app/data" \
    --env-file .env \
    -e DATABASE_PATH=/app/data/database.db \
    -e THUMBS_DIR=/app/data/thumbs \
    -e TEMP_DIR=/app/data/temp \
    --user 65532:65532 \
    ghcr.io/kanpief/mernorcloud:latest
```

---

### 2. Docker Compose (Recommended)

Run with:
```bash
docker compose up -d
```
