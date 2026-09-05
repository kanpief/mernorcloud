# 🛠️ Installation Guide / Hướng dẫn cài đặt

Hướng dẫn cài đặt MernorCloud (Zpiltk Edition) trên nhiều nền tảng (Windows, Linux, Docker, Termux, macOS, Raspberry Pi).  
Complete installation guide for MernorCloud (Zpiltk Edition) across various platforms.

---

## 🇻🇳 Tiếng Việt

### 1. Cài đặt tự động qua Script (Khuyên dùng)

Đây là cách đơn giản và nhanh nhất để cài đặt, cấu hình và quản trị MernorCloud. Script sẽ tự động cài đặt các phụ thuộc cần thiết (FFmpeg, yt-dlp, aria2, Cloudflared...), cấu hình dịch vụ chạy ngầm và cung cấp menu quản lý trực quan.

#### Trên Windows
1. Tải tệp [**`auto-install.bat`**](https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-install.bat) về thư mục bạn muốn cài đặt.
2. Click chuột phải vào tệp và chọn **Run as Administrator**.
3. Menu quản trị sẽ hỗ trợ:
    * Tự động cài đặt FFmpeg, yt-dlp & Cloudflared.
    * Tải phiên bản MernorCloud mới nhất.
    * Cấu hình Cloudflare Tunnel (gắn tên miền riêng HTTPS miễn phí).
    * Khởi động / Dừng ứng dụng chạy ngầm và xem nhật ký (log).

#### Trên Linux / Termux / macOS / Raspberry Pi
Script hỗ trợ Ubuntu, Debian, CentOS, AlmaLinux, Arch, macOS (Homebrew), Termux (Android) và ARM (Raspberry Pi).

```bash
# Sử dụng curl (Khuyên dùng)
curl -fsSL https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-setup.sh -o auto-setup.sh && bash auto-setup.sh

# Hoặc sử dụng wget
wget -qO auto-setup.sh https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-setup.sh && bash auto-setup.sh
```

**⚠️ Lưu ý cho Termux**: Nên cài đặt Termux từ [F-Droid](https://f-droid.org/packages/com.termux/) hoặc [GitHub Releases chính thức](https://github.com/termux/termux-app/releases).

---

### 2. Cài đặt thủ công (Binary)

#### Bước 1: Yêu cầu phụ thuộc
Cài đặt **FFmpeg**, **yt-dlp** và **aria2** (tùy chọn) để hỗ trợ đầy đủ xem trước video và tải ngầm:
* **Ubuntu/Debian**: `sudo apt update && sudo apt install -y ffmpeg python3 aria2`
* **RedHat/CentOS/Fedora**: `sudo dnf install -y ffmpeg python3 aria2`
* **Alpine Linux**: `apk add ffmpeg python3 yt-dlp aria2`
* **Windows**: Tải các binary FFmpeg, yt-dlp, aria2 và thêm vào biến môi trường PATH.

#### Bước 2: Khởi động và cấu hình
1. Tải bản binary phù hợp với hệ điều hành từ mục Releases của repository.
2. Khởi động ứng dụng:
   ```bash
   ./telecloud # Linux / macOS
   telecloud.exe # Windows
   ```
3. Mở trình duyệt và truy cập `http://localhost:8091/setup` để hoàn tất cấu hình ban đầu qua Web Setup Wizard.
   * **Lưu ý**: Thông tin Telegram API mặc định đã được tích hợp sẵn. Người dùng không cần nhập API ID/Hash trừ khi muốn sử dụng thông tin riêng tại phần *Cài đặt nâng cao*.

---

## 🇺🇸 English

### 1. Automatic Installation (Recommended)

#### On Windows
1. Download [**`auto-install-en.bat`**](https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-install-en.bat).
2. Right-click and choose **Run as Administrator**.
3. Use the menu to install dependencies, setup Cloudflare Tunnel, and manage the background service.

#### On Linux / Termux / macOS / Raspberry Pi
Supports Ubuntu, Debian, CentOS, Arch, macOS, Termux, and ARM devices:

```bash
# Using curl
curl -fsSL https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-setup-en.sh -o auto-setup-en.sh && bash auto-setup-en.sh

# Or using wget
wget -qO auto-setup-en.sh https://raw.githubusercontent.com/kanpief/mernorcloud/main/auto-setup-en.sh && bash auto-setup-en.sh
```

---

### 2. Manual Installation (Prebuilt Binary)

#### Step 1: System Requirements
* **Ubuntu/Debian**: `sudo apt update && sudo apt install -y ffmpeg python3 aria2`
* **Alpine Linux**: `apk add ffmpeg python3 yt-dlp aria2`
* **Windows**: Download FFmpeg, yt-dlp, and aria2 binaries and add them to PATH.

#### Step 2: Download & Startup
1. Download the executable binary for your OS from the Releases section.
2. Run the application:
   ```bash
   ./telecloud # Linux/macOS
   telecloud.exe # Windows
   ```
3. Access `http://localhost:8091/setup` in your browser to complete the Web Setup Wizard.
