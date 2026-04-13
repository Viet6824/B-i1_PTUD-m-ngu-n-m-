# Phần B: Cài đặt Ubuntu và Docker

Trong phần này, em tiến hành thiết lập môi trường máy chủ ảo hóa trên Windows bằng phần mềm VMware và cài đặt nền tảng Docker để chuẩn bị cho việc chạy các dịch vụ IOT.

## 1. Cài đặt Ubuntu và truy cập SSH
Em đã sử dụng VMware để giả lập máy chủ. Network Adapter được thiết lập ở chế độ NAT để Windows host có thể giao tiếp trực tiếp với máy ảo. 
Sau khi cài đặt xong Ubuntu 24.04.4 LTS (có cài kèm OpenSSH Server), em kiểm tra IP và tiến hành kết nối SSH từ CMD của Windows thành công.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bec15e51-7997-4f81-a3c0-ac2359801811" />


## 2. Tìm hiểu các lệnh cơ bản của Ubuntu
Em đã thực hành các lệnh thao tác với file và thư mục cơ bản trên môi trường Linux (mkdir, cd, cp, ls...). Việc nắm vững các lệnh này giúp em dễ dàng thao tác với các file cấu hình của Docker sau này.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/248a6d33-796a-4902-bbfd-b18a04733971" />


## 3. Cài đặt Docker và Docker Compose
Tiến hành cài đặt Docker Engine và Docker Compose. Đồng thời, em đã cấu hình phân quyền (thêm user hiện tại vào group `docker`) để có thể chạy các lệnh thao tác với container mà không cần phải gõ tiền tố `sudo` mỗi lần.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c1718091-c21d-4234-b1a6-d7a46751b6d3" />

## 4. Cấu hình Tường lửa (UFW)
Để bảo vệ máy chủ nhưng vẫn cho phép luồng dữ liệu của hệ thống IOT và Web đi qua, em đã sử dụng UFW để mở các cổng cần thiết theo yêu cầu, bao gồm:
* Port 80 (Nginx Web Server)
* Port 1880 (Node-RED)
* Port 9630 (Python Flask API)
* Port 22 (SSH)
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f671c570-08f2-482e-a4a5-271c641ee4fe" />

