# Group12-Social-Media-Website
Đồ án cuối kỳ môn Phát triển ứng dụng Web của Nhóm 12 - IT0001 - K50 (started from Jan 2026)
Bước 1: Sao chép Kho lưu trữ (Clone Repository):
git clone [https://github.com/Hacker3707/Group12-Social-Media-Website.git] (https://github.com/Hacker3707/Group12-Social-Media-Website.git)
cd Group12-Social-Media-Website.

Bước 2: Cài đặt composer tại đây 
composer install

Bước 3: Cấu hình biến môi trường:
Sao chép tệp môi trường mẫu:
cp .env.example .env
Chỉnh sửa .env với các cấu hình:
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost:3000
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=passo
DB_USERNAME=root
DB_PASSWORD=

CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

SUPABASE_URL=https://<your-project-id>.supabase.co
SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5c...
SUPABASE_JWT_SECRET=your-jwt-secret-from-api-settings

Bước 4: Tạo cơ sở dữ liệu:
Mở phpMyAdmin của Xampp vào phần SQL: Create Database passo;
Import file socialnetworkdb.sql vào phần import của phpMyAdmin

Bước 5: Cấu hình Cloudinary (Để lưu trữ ảnh avatar):
Đăng ký tài khoản miễn phí tại đây.
Lấy thông tin xác thực (credentials) từ bảng điều khiển.
Cập nhật file .env với những thông tin đó.

Bước 6: Cấu hình dịch vụ login Google:
Cấu hình Supabase và Google đám mây (Supabase & Google Cloud)
Thiết lập Supabase:
Truy cập vào trang chủ Supabase, tạo tài khoản miễn phí và tạo một project mới
Sao chép lại URL project vừa mới tạo
Ở thanh điều hướng bên trái, truy cập vào Authentication → Sign In/Providers
Ở phần Auth Providers bấm chọn Google, thiết lập Google Cloud Console để điền các thông tin cần thiết.
Thiết lập Google Cloud Console:
Truy cập vào trang chủ Google Cloud Console
Ở góc trái cạnh logo Google Cloud, chọn cửa sổ và chọn New project
Ở Project name, nhập tên dự án ví dụ passo, sau đó nhấn Create
Tiếp theo, bấm chọn vào dấu 3 gạch, chọn APIs & Services → OAuth consent screen
Ở Overview → Google Auth Platform not configured yet, chọn Get started
Ở App Information, điền App name ví dụ như passo, User support email chọn email hiện tại đang login, rồi nhấn Next
Ở phần Audience, chọn External, rồi nhấn Next
Ở Contact Information nhập email hiện tại đang login, nhấn Next rồi nhấn Create
Tạo Client ID:
Ở menu bên trái, chọn APIs & Services → Credentials
Trên cùng chọn Create credentials → OAuth client ID
Application type chọn Web application, ở Name đặt tên ví dụ như passo.
Ở phần Authorized redirect URIs, nhấn Add URL, sau đó quay lại Thiết lập Supabase, copy đường dẫn của phần Callback URL (for OAuth) rồi quay lại paste vào URLs 1, sau đó nhấn Create
Ngay sau khi nhấn tạo, Google sẽ hiển thị một bảng popup chứa 2 chuỗi mã: Client ID và Client Secret, copy 2 chuỗi này, quay trở lại (Authentication → Providers → Google), bật Enable Sign in with Google, dán 2 chuỗi này vào các ô tương ứng và nhấn Save
Khai báo URL cho Ứng dụng Web:
Quay lại Supabase, vào Authentication → URL Configuration
Site URL: Nhập http://localhost:3000
Redirect URLs: Thêm chính xác đường dẫn file xử lý callback trên hệ thống PHP. Ví dụ: http://localhost:3000/MVC/View/User/callback.php
Cập nhật tệp file .env với các thông tin của Supabase

Bước 7: Truy cập bằng đường dẫn: http://localhost:3000/ để chạy.
