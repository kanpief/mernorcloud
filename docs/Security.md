# 🔐 Security Policy & Hardening / Chính sách bảo mật & Hardening

Thông tin chi tiết về kiến trúc bảo mật, các biện pháp hardening và khuyến nghị vận hành an toàn cho MernorCloud (Zpiltk Edition).  
Detailed overview of the security architecture, hardening measures, and operational recommendations for MernorCloud (Zpiltk Edition).

---

## 🇻🇳 Tiếng Việt

### 1. Các biện pháp bảo mật mặc định (Hardening)

MernorCloud tích hợp sẵn các tiêu chuẩn bảo mật đa lớp nhằm bảo vệ tối đa dữ liệu của bạn:

*   **Mã hóa AES-256-GCM**: Toàn bộ session Telegram và các cấu hình nhạy cảm (`api_id`, `api_hash`, `log_group_id`, `bot_tokens`) đều được mã hóa bằng AES-256-GCM trước khi lưu vào Cơ sở dữ liệu.
*   **Bảo mật hệ thống (systemd & Linux)**: Script `auto-setup.sh` tạo systemd service chạy dưới user riêng, áp dụng các cờ cách ly bảo mật như `NoNewPrivileges=true`, `ProtectSystem=strict`, `ProtectHome=true`, `PrivateTmp=true`.
*   **Cơ chế ký HMAC cho tải trực tiếp**: Token tải trực tiếp (direct-download) được ký HMAC sử dụng khóa derived từ master key. Đổi mật khẩu admin sẽ **không** làm mất hiệu lực các liên kết tải trực tiếp đã được phát hành trước đó.
*   **Bảo vệ tệp chia sẻ có mật khẩu**: Sử dụng token session ngẫu nhiên đã ký lưu trong cookie. Mật khẩu hash Bcrypt tuyệt đối **không** bao giờ lưu trực tiếp hay gửi lại ở client.
*   **Bảo mật WebDAV**: Áp dụng giới hạn tần suất (rate limit 5 lần thử / 15 phút cho mỗi IP) để chống dò mật khẩu brute-force. Cache xác thực ngắn sử dụng chuỗi mã hóa SHA-256 của mật khẩu.
*   **Quản lý phiên đăng nhập (HTTP Session)**: Mỗi phiên làm việc đều có hạn dùng (mặc định 30 ngày). Khi đổi mật khẩu, toàn bộ các phiên đăng nhập khác của tài khoản đó lập tức bị vô hiệu hóa.
*   **Nhật ký hoạt động (Audit Log)**: Ghi lại đầy đủ các sự kiện quan trọng trong bảng `audit_log` (đăng nhập, đăng xuất, đổi mật khẩu, reset mật khẩu tài khoản con, thay đổi cài đặt hệ thống).
*   **Ngăn chặn tấn công SSRF (SafeHTTPClient)**: Trình tải từ xa (remote URL upload, yt-dlp) sử dụng client an toàn (`SafeHTTPClient`) thực hiện ghim IP động tại thời điểm kết nối, chặn hoàn toàn các cuộc tấn công DNS Rebinding tới dải IP riêng tư nội bộ.

### 2. Các khuyến nghị vận hành

*   **Bảo mật Telegram Cloud**: Hạ tầng lưu trữ đám mây của Telegram không phải là mã hóa đầu cuối (E2EE) cho tệp lưu trữ. Đối với các dữ liệu cực kỳ nhạy cảm, bạn có thể chủ động mã hóa ở phía client (ví dụ dùng `rclone crypt` hoặc Cryptomator) trước khi tải lên.
*   **Tài khoản vận hành**: Khuyến khích sử dụng tài khoản Telegram riêng / số điện thoại phụ để vận hành MernorCloud nhằm tối ưu quản lý và bảo vệ tài khoản cá nhân chính.

---

## 🇺🇸 English

### 1. Out-of-the-Box Security Measures

*   **AES-256-GCM Encryption**: Encrypted Telegram sessions and sensitive database values.
*   **System Hardening**: Isolated service execution with systemd hardening flags.
*   **HMAC Signed Downloads**: Robust direct download URL tokens verified with derived master keys.
*   **Brute-force Protected WebDAV**: In-memory rate limiting against unauthorized login attempts.
*   **SSRF Protection**: Dynamic DNS pinning and private IP filtering for remote downloaders.
*   **Audit Logging**: Comprehensive activity logs stored for administrative review.
