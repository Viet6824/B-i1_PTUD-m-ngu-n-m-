## G. Triển khai ứng dụng đến End-user (Cloudflare Tunnel)

Trong phần này, em thực hiện đưa ứng dụng từ môi trường máy ảo Local ra Internet bằng giải pháp Cloudflare Tunnel.

### 1. Thiết lập Cloudflare Tunnel trong Docker
Thay vì chạy lệnh thủ công, em đã tích hợp trực tiếp Cloudflare vào hệ thống thông qua `docker-compose.yml`. 

**Các bước thực hiện:**
* **Bước 1:** Tạo Tunnel trên bảng điều khiển Cloudflare Zero Trust và lấy `TUNNEL_TOKEN`.
* **Bước 2:** Khai báo Service `tunnel` trong file Compose để tự động kết nối khi hệ thống khởi động.
* **Bước 3:** Cấu hình Public Hostname trên Cloudflare trỏ về `http://mynginx:80`.

**Cấu hình trong docker-compose.yml:**
```yaml
  tunnel:
    image: cloudflare/cloudflared
    restart: always
    environment:
      - TUNNEL_TOKEN=${CF_TOKEN}
    command: tunnel run
```

### 2. Kết quả triển khai
Sau khi triển khai, ứng dụng đã có thể truy cập công khai qua tên miền (sub-domain) của Cloudflare mà không cần mở Port trên Router hay máy ảo.

* **Tên miền truy cập:** `http://your-subdomain.trycloudflare.com` (Hoặc tên miền riêng của bạn).
* **Kiểm tra thực tế:** Truy cập bằng mạng 4G trên điện thoại, trang web hiển thị đầy đủ giao diện và dữ liệu API từ Node-RED.

**Minh chứng hoạt động:** *(📸 Chèn ảnh màn hình trình duyệt điện thoại truy cập vào web qua link Cloudflare)*

---

### 3. Trả lời các câu hỏi về bài làm (Dành cho thầy vấn đáp)

1. **Tại sao dùng Nginx làm Reverse Proxy mà không trỏ thẳng Tunnel vào Node-RED?**
   * **Trả lời:** Nginx giúp quản lý tập trung các dịch vụ (Web tĩnh và API) trên cùng một cổng 80, tăng tính bảo mật và giúp URL gọn gàng hơn thay vì phải truy cập trực tiếp qua cổng 1880 của Node-RED.

2. **Sự khác biệt giữa Mount file và Mount thư mục?**
   * **Mount file:** Gắn một file cấu hình cụ thể (như `nginx.conf`), nội dung file trong container đồng bộ với máy host.
   * **Mount thư mục:** Gắn cả một thư mục (như `myweb`), giúp quản lý nhiều file cùng lúc và dữ liệu phát sinh trong thư mục đó được lưu lại trên máy host.

3. **Thay đổi index.html ở máy Ubuntu, web có đổi ngay không?**
   * **Trả lời:** **Có**. Vì chúng ta sử dụng `volumes` dạng Bind Mount, mọi thay đổi trên file ở máy host sẽ được cập nhật tức thì vào trong container mà không cần khởi động lại.

4. **Tại sao nên thêm hậu tố `:ro` khi mount Nginx?**
   * **Trả lời:** `:ro` (Read-only) giúp container Nginx chỉ có quyền đọc file cấu hình mà không có quyền sửa xóa, giúp tăng cường bảo mật cho máy host.

5. **Khi dùng Cloudflare Tunnel, có cần mở cổng (port) nữa không?**
   * **Trả lời:** **Không**. Cloudflare Tunnel tạo một kết nối ngược (outbound) từ máy ảo lên Cloudflare, do đó không cần mở port 80 hay 443 trên router, giúp bảo vệ hệ thống khỏi các cuộc tấn công dò tìm port.

---
