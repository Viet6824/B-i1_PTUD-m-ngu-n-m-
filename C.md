# Phần C: Cấu hình docker compose

Trong phần này, em đã xây dựng cấu trúc thư mục dự án và sử dụng Docker Compose để triển khai đồng thời 2 dịch vụ: Web Server (Nginx) và IOT Platform (Node-RED).

## 1. Cấu hình dịch vụ
- Em đã tạo thư mục `~/myapp` chứa file cấu hình trung tâm `docker-compose.yml`.
- **Nginx**: Chạy trên cổng 80, được mount thư mục `./myweb` chứa trang `index.html` (thông tin cá nhân) và file cấu hình `./nginx/nginx.conf`. File config này đóng vai trò Reverse Proxy, định tuyến các request `/api` sang Node-RED.
- **Node-RED**: Chạy trên cổng 1880, mount dữ liệu ra thư mục ngoài `./nodered` để dữ liệu không bị mất khi xóa container.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a9c85ff0-494b-4eaa-a7ce-5e79c713f033" />


## 2. Bảo mật Node-RED
Sau khi khởi chạy lần đầu để container sinh ra các file hệ thống, em đã can thiệp vào file `./nodered/settings.js`, kích hoạt khối lệnh `adminAuth` và sử dụng bcryptjs để mã hóa mật khẩu, bắt buộc người dùng phải đăng nhập mới có thể chỉnh sửa luồng IOT.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7886fe74-c38a-4d4f-ba08-044cd575f376" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/15f7f04b-2dd3-429f-bd02-7196885a7649" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f7d4e3fb-8080-46af-9acd-4cf9f2cf9bb3" />
