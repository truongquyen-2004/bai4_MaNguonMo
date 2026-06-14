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

-  Tạo Cloudflare Tunnel
-  Đăng nhập Cloudflare: cloudflared tunnel login
-  Tạo tunnel: cloudflared tunnel create wordpress-tunnel
-  Tạo file config tunnel: nano ~/.cloudflared/config.yml

<img width="1661" height="141" alt="Screenshot 2026-06-14 164355" src="https://github.com/user-attachments/assets/e890877b-fc3e-4813-acb7-44f3f18f8e9b" />

Add router DNS:

<img width="1027" height="126" alt="Screenshot 2026-06-14 214505" src="https://github.com/user-attachments/assets/c050174d-eb56-40d0-b645-4b89a28fea11" />

Chạy tunnel:

<img width="1027" height="407" alt="Screenshot 2026-06-14 175313" src="https://github.com/user-attachments/assets/481d492b-cc76-4a62-8878-8c9a05bd328f" />

Kiểm tra hoạt động:
-  Kiểm tra cơ sở dữ liệu trước khi cài WordPress

-  Đăng nhập PhpMyAdmin:

-  Server: mariadb
-  User: root
-  Password: rootpassword

<img width="1671" height="806" alt="image" src="https://github.com/user-attachments/assets/42a3a405-61df-4513-98bf-4a6b4ecf36b0" />

<img width="1711" height="797" alt="Screenshot 2026-06-14 215227" src="https://github.com/user-attachments/assets/92dea3c0-0b01-4dda-a32a-dde1c2f3d18e" />

<img width="1918" height="1078" alt="Screenshot 2026-06-14 201745" src="https://github.com/user-attachments/assets/39c5030b-9466-422f-94b6-8a544d676467" />

Quan sát:
-  Database wordpress_db đã tồn tại Chưa có bảng dữ liệu (do làm xong rồi mới chụp nên có các bảng của wordpress tự tạo).

<img width="1711" height="797" alt="Screenshot 2026-06-14 215227" src="https://github.com/user-attachments/assets/60469199-0d83-45f7-af25-7a3473a92932" />

Cài đặt WordPress
Truy cập:
Làm theo hướng dẫn:

Sau khi cài xong:

-  WordPress sẽ tự tạo toàn bộ bảng dữ liệu

-  Kiểm tra database sau khi cài WordPress

-  Vào lại PhpMyAdmin.

Quan sát:

<img width="1711" height="797" alt="Screenshot 2026-06-14 215227" src="https://github.com/user-attachments/assets/6634491c-7801-44cf-aa4f-f65914f046f5" />



