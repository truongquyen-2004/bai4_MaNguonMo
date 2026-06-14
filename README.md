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

Tạo bài viết thủ công
-  Bài viết 1

-  Giới thiệu bản thân:

  <img width="1778" height="942" alt="Screenshot 2026-06-14 172124" src="https://github.com/user-attachments/assets/c9eebf88-89da-44a0-8495-394d62ccb2da" />
  Bài viết 2

Giới thiệu kiến thức đã học ở môn Phát triển ứng dụng với mã nguồn mở

<img width="936" height="250" alt="image" src="https://github.com/user-attachments/assets/9aac0126-0341-4c93-9f2e-682bd13dba79" />

Cấu hình n8n
-  Tạo tài khoản admin
Điền:
-  Email đúng
-  Password
-  sau khi làm xong chúng ta se được đưa đến màn hình trang chủ

<img width="1486" height="640" alt="image" src="https://github.com/user-attachments/assets/dcc39b0f-1a34-4c24-a612-b1cf6ec2432d" />

Activate License Key:

vào trang chủ => SETTING (góc dưới trái) => Usage and plan => Enter activation key

<img width="1917" height="1067" alt="Screenshot 2026-06-14 193658" src="https://github.com/user-attachments/assets/2118ed69-eb7f-40f1-85fe-d18f033abdb7" />

n8n sẽ gửi mail chứa KEY.

<img width="1022" height="460" alt="image" src="https://github.com/user-attachments/assets/bc87b5bf-edf9-4846-b941-08d35875717e" />
nhập key vào sau đó nhấn Activate

Activate xong.

Tạo Telegram Bot (mặc định là đã có tài khoản Telegram)
Chat với: @BotFather

nhập /newbot

Đặt:

Tên bot
Username bot
sau đó BotFather sẽ gửi cho 1 HTTP API TOKEN

<img width="1792" height="795" alt="Screenshot 2026-06-14 215423" src="https://github.com/user-attachments/assets/9f135f1a-3ac9-49dd-bb54-af7d04002a2e" />

Quy trình hoạt động:

Điện thoại → Telegram Bot → Telegram Trigger → Gemini AI → JavaScript xử lý JSON → WordPress Create Post → Bài viết tự động xuất hiện trên website

Kiểm tra kết quả Từ điện thoại

Nhắn:

Viết 1 đoạn văn 200 chữ nói về lợi ích của việc đi học

Sau vài giây:

WordPress có bài viết mới

Có HTML + CSS đẹp

Đăng tự động

<img width="1840" height="920" alt="Screenshot 2026-06-14 215403" src="https://github.com/user-attachments/assets/04339fef-28fa-48b8-8072-fdacc11d1f31" />

Nhận xét thành quả đạt được
Sau khi hoàn thành bài tập:

-  Hiểu cách triển khai hệ thống bằng Docker Compose
-  Biết sử dụng MariaDB cho WordPress
-  Sử dụng Cloudflare Tunnel để public service
-  Biết cấu hình n8n automation
-  Kết nối Telegram với AI Gemini
-  Tự động tạo và đăng bài WordPress bằng AI
-  Hiểu quy trình xử lý dữ liệu JSON trong n8n
-  Có thể mở rộng thành hệ thống AI Content Automation thực tế
Kết luận
Bài tập giúp hiểu rõ:

Docker
-  Container networking
-  WordPress deployment
-  Cloudflare Tunnel
-  n8n automation
-  Telegram Bot API
-  Gemini AI API
-  Workflow tự động hóa bằng AI
Đây là mô hình rất thực tế và có thể phát triển thành hệ thống tạo nội dung tự động hoàn chỉnh.






