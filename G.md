## G. Triển khai ứng dụng đến End-user (Cloudflare Tunnel)

Trong phần này, em thực hiện đưa ứng dụng từ môi trường máy ảo Local ra Internet bằng giải pháp Cloudflare Tunnel.

### 1. Thiết lập Cloudflare Tunnel trong Docker
Thay vì chạy lệnh thủ công, em đã tích hợp trực tiếp Cloudflare vào hệ thống thông qua `docker-compose.yml`. 

**Các bước thực hiện:**
* **Bước 1:** Tạo Tunnel trên bảng điều khiển Cloudflare Zero Trust và lấy `TUNNEL_TOKEN`.
* **Bước 2:** Khai báo Service `tunnel` trong file Compose để tự động kết nối khi hệ thống khởi động.
* **Bước 3:** Cấu hình Public Hostname trên Cloudflare trỏ về `http://mynginx:80`.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6ff26a48-7bd2-42e4-877b-16f5fea476dd" />

**Cấu hình trong docker-compose.yml:**
```yaml
 tunnel:
    image: cloudflare/cloudflared:latest
    restart: always
    command: tunnel run --token DÁN_MÃ_TOKEN
```

### 2. Kết quả triển khai
Sau khi triển khai, ứng dụng đã có thể truy cập công khai qua tên miền (sub-domain) của Cloudflare

<img width="1260" height="2800" alt="image" src="https://github.com/user-attachments/assets/bdf1b398-7d90-43c9-9455-df4efbb474f5" />


