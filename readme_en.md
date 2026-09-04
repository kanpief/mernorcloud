# MernorCloud (Zpiltk)

<div align="center">

**High-performance Telegram-backed Unlimited Cloud Storage written in Golang.**

</div>

---

## ✨ Key Features

* 📁 **Unlimited Storage**: Store files directly on Telegram with no file size limits (auto file chunking).
* 🎬 **Media & Subtitles Streaming**: Stream video and music directly on the web with subtitle support (`.srt`, `.vtt`, `.ass`).
* 📚 **Built-in Document & Comic Reader**: Read **EPUB**, **CBZ** comics, and **PDF** documents directly in browser.
* 🔗 **Flexible Sharing**: Public share links and direct download links for files and **folders** with password protection.
* ⚡ **On-The-Fly Folder Download**: Real-time ZIP streaming for full folders without consuming server disk space.
* 🗂️ **Modern File Browser**: Clean **Grid** and **List** views, complete with a trash bin for file recovery.
* 📂 **WebDAV & S3 API**: Mount as a network drive or connect with Rclone, Cyberduck, Infuse, etc.
* 📥 **URL, Video & Torrent Downloader**: Integrated `yt-dlp` and `aria2c` for background downloads.
* 👥 **Multi-User**: Isolated virtual workspaces for sub-accounts.
* 🤖 **Multi-Bot (Bot Pool)**: Distribute workloads across multiple Telegram bots for maximum throughput.
* 🔐 **Passkey Security & Encryption**: Biometric login (Fingerprint, FaceID) and AES-256-GCM data encryption.
* 🗄️ **Multi-Database**: Full support for **SQLite**, **PostgreSQL**, and **MySQL**.

---

## 🚀 Quick Start

### 1. Docker Deployment (Recommended)

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

Or using `docker-compose.yml`:
```bash
docker compose up -d
```

### 2. Deploy on Render / Cloud PaaS
1. Create a Web Service with runtime **Docker**.
2. Add environment variables:
   - `TELECLOUD_MASTER_KEY`: *[64-character hex master key]*
   - `DATABASE_DRIVER`: `postgres`
   - `DATABASE_DSN`: *[PostgreSQL connection URL]*
   - `TEMP_DIR`: `/tmp`
3. Deploy and open the web URL to complete initial admin setup.

---

## ⚙️ Configuration

Copy `env.example` to `.env` to configure:

```env
# Encryption Master Key (32-byte hex)
TELECLOUD_MASTER_KEY=

# Server HTTP Port (Default: 8091)
PORT=8091

# Concurrent upload threads
TG_UPLOAD_THREADS=2

# Database settings (sqlite / postgres / mysql)
DATABASE_DRIVER=sqlite
DATABASE_PATH=data/database.db
```

---

## 📜 License

Released under the [GNU Affero General Public License v3.0 (AGPL-3.0)](https://www.gnu.org/licenses/agpl-3.0.html).
