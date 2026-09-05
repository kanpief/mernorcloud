# 🛠️ Development & Build Guide / Hướng dẫn Phát triển & Build

Hướng dẫn chi tiết dành cho nhà phát triển muốn tự biên dịch MernorCloud (Zpiltk Edition) từ mã nguồn hoặc tùy biến giao diện/bản dịch.  
Guide for developers who want to build MernorCloud (Zpiltk Edition) from source or customize the UI and translations.

---

## 🇻🇳 Tiếng Việt

### 1. Biên dịch từ nguồn (Build from Source)

#### Cách 1: Build bằng Docker (Khuyên dùng)
Docker sẽ tự động xử lý toàn bộ quy trình biên dịch frontend và backend mà không cần cài đặt Golang hay Bun trên máy:

1. Clone kho lưu trữ:
   ```bash
   git clone https://github.com/kanpief/mernorcloud.git
   cd mernorcloud
   ```
2. Build image cục bộ:
   ```bash
   docker build -t mernorcloud:local .
   ```
3. Khởi chạy container:
   ```bash
   docker run -d -p 8091:8091 -v "$(pwd)/data:/app/data" --env-file .env mernorcloud:local
   ```

---

#### Cách 2: Build thủ công (Native)
Yêu cầu hệ thống:
* **Golang 1.24+**: [https://go.dev](https://go.dev)
* **Bun**: [https://bun.sh](https://bun.sh) (dùng để bundle frontend)

Các bước thực hiện:
1. **Biên dịch Frontend**:
   ```bash
   cd web
   bun install
   bun run build.js
   cd ..
   # Hoặc chạy lệnh: make frontend (nếu có make)
   ```
2. **Biên dịch Backend (Go)**:
   ```bash
   go mod tidy
   go build -o telecloud
   ```

##### Nhúng thông tin API Telegram mặc định khi biên dịch:
Để nhúng sẵn Telegram `API_ID` và `API_HASH` vào binary khi phát hành:
1. Định nghĩa `API_ID` và `API_HASH` trong tệp `.env` cục bộ.
2. Biên dịch bằng `make`:
   ```bash
   make build
   ```
3. Hoặc biên dịch trực tiếp bằng `go build`:
   ```bash
   go build -ldflags="-X telecloud/config.DefaultAPIIDStr=YOUR_API_ID -X telecloud/config.DefaultAPIHash=YOUR_API_HASH" -o telecloud
   ```

---

### 2. Tùy biến Bản dịch & Giao diện (Localization)

Toàn bộ mã nguồn giao diện và các tệp ngôn ngữ nằm trong thư mục `web/`:
1. Các tệp từ điển ngôn ngữ định dạng JSON nằm ở `web/static/locales/` (ví dụ: `vi.json`, `en.json`, `zh.json`, `ru.json`...).
2. Để thêm ngôn ngữ mới:
   - Tạo tệp `web/static/locales/<mã_ngôn_ngữ>.json` (sao chép từ `en.json` và dịch các giá trị).
   - Đăng ký ngôn ngữ trong mảng `availableLangs` tại `web/static/js/common.js`.
   - Chạy lệnh `bun run build.js` trong thư mục `web/` để nén các bản dịch vào binary.

---

### 3. Quy chuẩn Cơ sở dữ liệu (SQL) & Khóa mã hóa

#### Khóa mã hóa (`master.key`):
* Để tránh xung đột đường dẫn lưu trữ khóa `master.key` khi thư mục `data` được tạo sau khi ứng dụng khởi chạy, toàn bộ mã nguồn sử dụng helper `utils.GetMasterKeyFilePath()`.
* Không viết kiểm tra tệp đường dẫn cứng để đảm bảo tương thích khi chạy đa nền tảng và đa Database (SQLite, MySQL, PostgreSQL).

#### Quy tắc tương thích cơ sở dữ liệu:
* Khi viết các câu truy vấn SQL liên quan tới kiểu logic (`BOOLEAN`):
  * **KHÔNG ĐƯỢC** gán hoặc so sánh trực tiếp với số nguyên (`1` hoặc `0`).
  * **BẮT BUỘC** sử dụng các từ khóa SQL tiêu chuẩn là `TRUE` và `FALSE` để đảm bảo tương thích tốt nhất trên cả SQLite, MySQL và cơ chế so khớp kiểu dữ liệu nghiêm ngặt của PostgreSQL.

---

## 🇺🇸 English

### 1. Build from Source

#### Method 1: Docker Build (Recommended)
1. Clone the repository:
   ```bash
   git clone https://github.com/kanpief/mernorcloud.git
   cd mernorcloud
   ```
2. Build local image:
   ```bash
   docker build -t mernorcloud:local .
   ```
3. Run container:
   ```bash
   docker run -d -p 8091:8091 -v "$(pwd)/data:/app/data" --env-file .env mernorcloud:local
   ```

---

#### Method 2: Manual Native Build
1. Install **Golang 1.24+** and **Bun** ([bun.sh](https://bun.sh)).
2. Build frontend assets:
   ```bash
   cd web && bun install && bun run build.js && cd ..
   ```
3. Build Go backend:
   ```bash
   go mod tidy
   go build -o telecloud
   ```

##### Embedding default Telegram API credentials:
```bash
go build -ldflags="-X telecloud/config.DefaultAPIIDStr=YOUR_API_ID -X telecloud/config.DefaultAPIHash=YOUR_API_HASH" -o telecloud
```

---

### 2. Localization & Frontend Customization
1. Locale JSON files are stored in `web/static/locales/`.
2. Add new languages or refine existing strings.
3. Re-bundle assets using `cd web && bun run build.js`.
