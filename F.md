## F. Gỡ lỗi và Tối ưu hóa hệ thống
Trong phần này, em thực hiện các thao tác quản trị để đảm bảo hệ thống vận hành ổn định và xử lý các tình huống phát sinh khi triển khai Docker Compose.
### 1. Quy trình gỡ lỗi hệ thống (Debugging)
Khi triển khai dự án, em thực hiện các bước sau để kiểm soát lỗi:
* **Kiểm tra trạng thái dịch vụ:** Gõ lệnh `docker compose ps` để biết container nào đang chạy (Up) hoặc cái nào bị lỗi (Exit/Restarting) để kịp thời sửa lỗi.
* **Xem nhật ký lỗi chi tiết:** Sử dụng lệnh `docker logs mynginx` hoặc `docker logs mynodered` để đọc thông báo lỗi từ hệ thống (ví dụ: lỗi cấu hình Nginx hoặc lỗi kết nối mạng).
* **Quan sát tài nguyên thực tế:** Sử dụng lệnh `docker compose stats` để giám sát lượng RAM và CPU mà mỗi service đang chiếm dụng, tránh việc máy ảo bị treo do quá tải.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c2354dc0-84bc-41ac-b631-2d7f3e44ca41" />

### 2. Thiết lập Healthcheck (Kiểm tra sức khỏe)
Em đã thêm cấu hình `healthcheck` vào file `docker-compose.yml` để hệ thống tự động kiểm tra trạng thái hoạt động của service:
* **Cách thực hiện:** Thiết lập lệnh `curl` kiểm tra cổng `1880` của Node-RED định kỳ.
* **Lợi ích:** Giúp Docker tự động phát hiện nếu Node-RED bị treo và hiển thị trạng thái `unhealthy` để em kịp thời khởi động lại.

```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:1880"]
  interval: 30s
  timeout: 10s
  retries: 3
```

### 3. Giới hạn tài nguyên (Resource Limits)
Để đảm bảo tính ổn định cho toàn bộ máy ảo Ubuntu, em đã thiết lập giới hạn cứng cho việc sử dụng bộ nhớ:
* **Cách thực hiện:** Thêm cấu hình `deploy.resources.limits.memory` vào dịch vụ trong file `.yml`.
* **Giới hạn:** Quy định mức tối đa là **512M** cho Node-RED.
* **Kết quả:** Ngăn chặn tình trạng một dịch vụ chiếm dụng quá nhiều RAM làm sập các dịch vụ khác hoặc sập máy ảo.

```yaml
deploy:
  resources:
    limits:
      memory: 512M
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bcb65b12-fab2-429b-b422-fdbc09da9294" />

### 4. Tối ưu cấu hình mạng nội bộ
Em đã cấu hình để tất cả các services (`mynginx`, `mynodered`, `tunnel`) đều dùng chung một mạng (network) nội bộ của Docker. Việc này giúp các container có thể gọi tên nhau (Service Name) thay vì dùng địa chỉ IP, giúp hệ thống linh hoạt và bảo mật hơn khi triển khai thực tế.
