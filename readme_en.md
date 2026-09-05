# MernorCloud (Zpiltk Edition)

<div align="center">

**High-Performance Unlimited Cloud Storage via Telegram — Customized & Optimized by Zpiltk.**

[![Go Version](https://img.shields.io/badge/Go-1.24+-00ADD8?style=flat&logo=go)](https://golang.org)
[![License: AGPL-3.0](https://img.shields.io/badge/License-AGPL--3.0-blue.svg)](https://www.gnu.org/licenses/agpl-3.0.html)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=flat&logo=docker)](https://www.docker.com/)
[![WebDAV](https://img.shields.io/badge/Protocol-WebDAV%20%7C%20S3-orange.svg)](#-key-features)
[![Telegram](https://img.shields.io/badge/Storage-Telegram%20MTProto-2CA5E0?style=flat&logo=telegram)](https://telegram.org)

</div>

---

## 📖 Overview

**MernorCloud (Zpiltk Edition)** is a next-generation personal cloud storage platform that turns your Telegram account into an unlimited, high-speed cloud drive.

Customized, maintained, and heavily optimized by **Zpiltk**:
- **Independent & Private**: A dedicated, customized edition providing enhanced privacy and control.
- **Performance Optimized**: Multi-chunk read-ahead prefetching, dynamic multi-bot load balancing, and real-time on-the-fly ZIP streaming without server disk overhead.
- **Self-Service Cookie Management**: Per-user upload and deletion of `yt-dlp` cookies for YouTube and protected media downloads.
- **Open Protocols**: Full WebDAV and S3 API compatibility for mounting network drives on Windows, macOS, Linux, or connecting with Infuse, Rclone, and Cyberduck.

---

## ✨ Key Features

### 🚀 Storage & Speed
* 📁 **Unlimited Telegram Storage**: Store files of any size without limitations. Large files are automatically split and assembled safely.
* 🤖 **Multi-Bot Pool**: Distribute concurrent transfers across multiple secondary bots for maximum upload and download speeds.
* ⚡ **On-The-Fly ZIP Streaming**: Download entire folders as `.zip` archives streamed directly from Telegram without creating temporary disk files on the server.

### 🎬 Media Streaming & Document Reader
* 🎥 **Web Media Player**: High-definition video and audio player with subtitle support (`.srt`, `.vtt`, `.ass`) and playback memory.
* 📖 **Built-in Document Readers**: Clean, embedded readers for **EPUB** eBooks, **CBZ** comics, and **PDF** documents.

### 🌐 Connectivity & Integrations
* 📂 **WebDAV & S3 API**: Mount as a network drive or sync seamlessly with Rclone, Infuse, Cyberduck, and Nextcloud.
* 📥 **URL, Video & Torrent Downloader**: Background downloader powered by `yt-dlp` and `aria2c` for direct and magnet links.
* 🍪 **Custom Cookie Management**: Each user can upload their own cookies to access age-restricted or private videos, with easy removal anytime.

### 👥 Security & Administration
* 👥 **Multi-User Isolation**: Independent sub-accounts with private workspaces and permission controls.
* 🔐 **Passkey & Biometric Authentication**: WebAuthn support for Fingerprint, TouchID, FaceID, and Windows Hello.
* 🛡️ **AES-256-GCM Encryption**: Encrypted Telegram sessions and sensitive database parameters at rest.
* 🗄️ **Multi-Database Support**: Out-of-the-box compatibility with **SQLite** (default), **PostgreSQL**, and **MySQL**.

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
    ghcr.io/kanpief/mernorcloud:latest
```

Or using `docker-compose.yml`:

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

Start container:
```bash
docker compose up -d
```

---

### 2. Automated Linux / VPS / Termux Installation

```bash
# Using cURL
curl -fsSL https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-setup-en.sh -o auto-setup-en.sh && bash auto-setup-en.sh

# Or using wget
wget -qO auto-setup-en.sh https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-setup-en.sh && bash auto-setup-en.sh
```

---

### 3. Windows Installation

1. Download [`auto-install-en.bat`](https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-install-en.bat).
2. Right-click and choose **Run as Administrator**.
3. Use the menu to install dependencies, setup Cloudflare Tunnel, and launch the service in the background.

---

### 4. Deploy on Render / PaaS Cloud

1. Create a **Web Service** with runtime **Docker**.
2. Add environment variables:
   - `TELECLOUD_MASTER_KEY`: *[64-character random hex string]*
   - `DATABASE_DRIVER`: `postgres`
   - `DATABASE_DSN`: *[PostgreSQL Connection URL]*
   - `TEMP_DIR`: `/tmp`
3. Deploy and open `http://<your-service-url>/setup` to complete initial setup.

---

## ⚙️ Environment Variables (`.env`)

Copy `env.example` to `.env` to configure:

```env
# Encryption master key for sensitive data (32-byte hex)
TELECLOUD_MASTER_KEY=

# HTTP server port (Default: 8091)
PORT=8091

# Listening address (Default: 0.0.0.0)
LISTEN_ADDR=0.0.0.0

# Concurrent upload threads per part (Default: 2)
TG_UPLOAD_THREADS=2

# Download read-ahead chunk prefetching (2 - 16, Default: 4)
TG_DOWNLOAD_PREFETCH=4

# Database driver: sqlite | postgres | mysql
DATABASE_DRIVER=sqlite
DATABASE_PATH=data/database.db
```

---

## 📚 Documentation

* 🛠️ [Installation Guide](docs/Installation.md)
* ⚙️ [Configuration Guide](docs/Configuration.md)
* 🐳 [Advanced Docker Deployment](docs/Docker.md)
* 🔌 [REST API Documentation](docs/API.md)
* 🔐 [Security & Hardening Policy](docs/Security.md)
* 💻 [Development & Source Build Guide](docs/Development.md)

---

## 📜 License

Released under the [GNU Affero General Public License v3.0 (AGPL-3.0)](https://www.gnu.org/licenses/agpl-3.0.html).  
Customized & developed by **Zpiltk**.
