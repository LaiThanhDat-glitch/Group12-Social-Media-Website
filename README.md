# Group12-Social-Media-Website

**Passo** là website mạng xã hội hỗ trợ chia sẻ bài đăng, tương tác, theo dõi người dùng, nhóm, trò chuyện và đăng nhập bằng Google. Đây là đồ án cuối kỳ môn Phát triển ứng dụng Web của Nhóm 12 – IT0001 – K50.

## Công nghệ sử dụng

- PHP 8.2 và mô hình MVC
- MySQL hoặc MariaDB
- Composer, `vlucas/phpdotenv`, Cloudinary PHP SDK và Guzzle
- Supabase Auth kết hợp Google OAuth

## Yêu cầu

- PHP 8.2 trở lên, bật các extension `mysqli` và `curl`
- Composer
- MySQL hoặc MariaDB (XAMPP có thể dùng để cài PHP và MariaDB)
- Tài khoản Cloudinary nếu muốn sử dụng chức năng tải ảnh
- Dự án Supabase và thông tin Google OAuth nếu muốn sử dụng đăng nhập Google

## Cài đặt và chạy local

### 1. Clone mã nguồn và cài thư viện

```bash
git clone https://github.com/Hacker3707/Group12-Social-Media-Website.git
cd Group12-Social-Media-Website
composer install
```

### 2. Tạo database và nạp dữ liệu

Tạo database tên `socialnetworkdb` trong phpMyAdmin hoặc MySQL:

```sql
CREATE DATABASE socialnetworkdb CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

Chọn database `socialnetworkdb` trong phpMyAdmin rồi import tệp [`socialnetworkdb.sql`](socialnetworkdb.sql). Tệp dump tạo các bảng nhưng không tự tạo hoặc chọn database.

### 3. Cấu hình môi trường

Tạo tệp `.env` ở thư mục gốc của dự án bằng cách sao chép `.env.example`:

```bash
cp .env.example .env
```

Trên Windows PowerShell, có thể dùng:

```powershell
Copy-Item .env.example .env
```

Thêm cấu hình MySQL và cập nhật thông tin dịch vụ trong `.env`:

```dotenv
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost:3000

DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=socialnetworkdb
DB_USERNAME=root
DB_PASSWORD=

CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

SUPABASE_URL=https://your-project-id.supabase.co
SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_JWT_SECRET=your_supabase_jwt_secret
```

Điền đúng thông tin đăng nhập MySQL của máy bạn. Lấy các biến Cloudinary từ **Cloudinary Console**. Lấy URL, anon key và JWT secret từ phần API/Project Settings của Supabase. Không commit hoặc chia sẻ tệp `.env` vì tệp này chứa thông tin bí mật.

### 4. Khởi động website

Từ thư mục gốc của dự án, chạy PHP development server:

```bash
php -S localhost:3000
```

Mở [http://localhost:3000](http://localhost:3000) trên trình duyệt. Đảm bảo MySQL/MariaDB đang chạy và database đã được nạp trước khi truy cập.

> Có thể dùng Apache của XAMPP thay cho PHP development server. Trong trường hợp đó, đặt dự án trong thư mục web của Apache, bật `mod_rewrite`, cho phép `.htaccess` bằng `AllowOverride All`, và cập nhật `APP_URL` cùng callback URL theo địa chỉ thực tế.

## Thiết lập dịch vụ tùy chọn

### Tải ảnh với Cloudinary

1. Tạo tài khoản tại [Cloudinary](https://cloudinary.com/).
2. Sao chép Cloud name, API Key và API Secret từ Cloudinary Console.
3. Điền các giá trị vào `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY` và `CLOUDINARY_API_SECRET` trong `.env`.

### Đăng nhập Google qua Supabase

1. Tạo project tại [Supabase](https://supabase.com/) và lấy Project URL, anon key, JWT secret.
2. Trong Supabase, mở **Authentication → Sign In / Providers → Google** và bật Google provider.
3. Tạo OAuth Client ID loại **Web application** trong [Google Cloud Console](https://console.cloud.google.com/). Thêm **Callback URL (for OAuth)** do Supabase cung cấp vào **Authorized redirect URIs** của Google, sau đó nhập Client ID và Client Secret vào cấu hình Google provider trong Supabase.
4. Trong Supabase, mở **Authentication → URL Configuration**. Đặt **Site URL** là `http://localhost:3000` và thêm URL callback ứng dụng vào **Redirect URLs**:

   ```text
   http://localhost:3000/MVC/View/User/callback.php
   ```

5. Điền `SUPABASE_URL`, `SUPABASE_ANON_KEY` và `SUPABASE_JWT_SECRET` trong `.env`.

Nếu chạy trên host hoặc cổng khác, cập nhật `APP_URL`, **Site URL** và **Redirect URLs** cho khớp. URL callback của ứng dụng luôn có dạng `<APP_URL>/MVC/View/User/callback.php`.

## Cấu trúc chính

```text
MVC/Controller/     Xử lý yêu cầu và luồng nghiệp vụ
MVC/Model/          Truy vấn và thao tác dữ liệu
MVC/View/           Giao diện PHP
MVC/Service/        Tích hợp Cloudinary và Supabase
Entity/             Các lớp mô hình dữ liệu
Module/             Cấu hình ứng dụng và upload
Procedures/         Các thủ tục SQL
socialnetworkdb.sql Cấu trúc và dữ liệu mẫu của database
index.php           Điểm vào và bộ định tuyến ứng dụng
```

## Development Team

| Member            | Role        |
| ----------------- | ----------- |
| Võ Nguyễn Ngọc Hà | Team leader |
| Mai Ngọc Ánh      | Member      |
| Hồ Minh Khang     | Member      |
| Lại Thành Đạt     | Member      |
