# MernorCloud Frontend Assets (Zpiltk Edition)

Thư mục này chứa mã nguồn giao diện web (HTML Templates, Tailwind CSS, Alpine.js, ESBuild) cho MernorCloud (Zpiltk Edition).  
This directory contains the source code for the MernorCloud (Zpiltk Edition) web interface.

## 📁 Cấu trúc thư mục / Directory Structure
- `templates/`: Go HTML templates.
- `static/`: Frontend assets (CSS, JS, Fonts, Images).
- `static/locales/`: Các tệp từ điển ngôn ngữ JSON (JSON translation files).
- `tailwind.config.js`: Cấu hình Tailwind CSS.
- `package.json`: Dependencies và build scripts.
- `build.js`: Unified build engine (Tailwind, esbuild, sync/minify locales, download static libs).
- `sync_locales.js`: Utility script to sync missing translation keys from `en.json` into all other locale files.

---

## 🛠️ Biên dịch Frontend / Build Process

Yêu cầu: Đã cài đặt **[Bun](https://bun.sh/)**.

1. Cài đặt thư viện:
   ```bash
   bun install
   ```
2. Biên dịch & bundle:
   ```bash
   bun run build.js
   ```

*Hoặc sử dụng các script tiện ích:*
* **Linux/macOS**: `./build-frontend.sh`
* **Windows (PowerShell)**: `.\build-frontend.ps1`
* **Windows (CMD)**: `build-frontend.bat`

---

Customized & Optimized by **Zpiltk**.
