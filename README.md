# bai4_MaNguonMo
Bài tập 04 của sinh viên: K225480106083 - Trương văn Quyến - môn Phát Triển Ứng Dụng Mã Nguồn Mở

KHAI THÁC N8N ĐỂ TỰ ĐỘNG ĐĂNG BÀI LÊN WORDPRESS
Mục tiêu
Sử dụng Docker trên Ubuntu để triển khai hệ thống gồm:

-  MariaDB
-  PhpMyAdmin
-  ordPress
-  Cloudflared Tunnel
-  n8n
Sau đó:

Public các service bằng Cloudflare Tunnel
Cài đặt WordPress
Tạo bài viết thủ công
Tạo workflow tự động đăng bài bằng AI thông qua Telegram → Gemini → n8n → WordPress
Chuẩn bị môi trường
Hệ điều hành: Ubuntu Server 24.04

Đã cài: Docker, Docker Compose, Domain trên Cloudflare

Tạo thư mục project
mkdir ~/wordpress
cd ~/wordpress
Tạo file docker-compose.yml
Tạo file:

<img width="806" height="773" alt="image" src="https://github.com/user-attachments/assets/08295c79-10f9-464b-b9b2-f174335ced36" />

chèn ảnh

-  Chạy Docker Compose
docker compose up -d

<img width="1046" height="528" alt="Screenshot 2026-06-14 174158" src="https://github.com/user-attachments/assets/33c1b4ba-3b2c-4846-aa9c-45745cc73c8c" />
Kiểm tra container:
Tạo Cloudflare Tunnel
Đăng nhập Cloudflare: cloudflared tunnel login
Tạo tunnel: cloudflared tunnel create wordpress-tunnel
Tạo file config tunnel: nano ~/.cloudflared/config.yml

<img width="1661" height="141" alt="Screenshot 2026-06-14 164355" src="https://github.com/user-attachments/assets/e890877b-fc3e-4813-acb7-44f3f18f8e9b" />

