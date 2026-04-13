# Trả lời câu hỏi 

#### Q1: Tại sao phải dùng Nginx làm Reverse Proxy mà không trỏ thẳng Tunnel vào Node-RED?
* **Trả lời:** Nginx đóng vai trò là "người điều phối", giúp quản lý tập trung cả Web tĩnh và Node-RED trên cùng một cổng 80. Nó giúp tăng tính bảo mật, dễ dàng mở rộng và tạo URL chuyên nghiệp hơn.

#### Q2: Sự khác biệt giữa việc Mount file và Mount thư mục trong Docker là gì?
* **Mount file:** Gắn duy nhất một file cấu hình từ máy host vào container (ví dụ: `nginx.conf`).
* **Mount thư mục:** Gắn toàn bộ folder (ví dụ: `/nodered`). Thường dùng để lưu trữ dữ liệu bền vững (Persistent Data), đảm bảo khi container bị xóa, dữ liệu vẫn còn trên máy host.

#### Q3: Nếu thay đổi file index.html ở máy Ubuntu, nội dung trên web có thay đổi ngay không? Tại sao?
* **Trả lời:** **Có**. Vì chúng ta sử dụng cơ chế **Bind Mount**. File bên trong container và máy host thực chất là một, Nginx sẽ đọc trực tiếp dữ liệu mới nhất từ ổ đĩa khi có yêu cầu truy cập.

#### Q4: Thuộc tính `restart: always` và `restart: unless-stopped` để làm gì?
* **restart: always:** Tự động khởi động lại container nếu nó bị lỗi hoặc khi máy ảo khởi động lại.
* **restart: unless-stopped:** Tương tự như `always`, nhưng nếu người dùng chủ động dừng container bằng lệnh `docker stop`, nó sẽ không tự bật lại khi khởi động máy ảo.

#### Q5: Cách khai báo để các services dùng chung 1 network và lợi ích?
* **Khai báo:** Thêm khối `networks:` ở cuối file và khai báo network đó trong từng service.
* **Lợi ích:** Các service giao tiếp với nhau bằng tên (DNS nội bộ), tăng tính bảo mật và cô lập hệ thống khỏi mạng bên ngoài.

#### Q6: Tại sao việc đưa Token vào `.env` và dùng `.gitignore` lại quan trọng về bảo mật?
* **Trả lời:** Giúp tránh lộ mã Token (mật khẩu của đường hầm) khi đẩy code lên GitHub công khai. Nếu lộ Token, kẻ xấu có thể chiếm quyền điều khiển đường hầm và tấn công vào máy ảo của bạn.

#### Q7: Tại sao nên thêm hậu tố `:ro` khi mount file cấu hình Nginx?
* **Trả lời:** `:ro` (Read-only) có nghĩa là "chỉ đọc". Điều này ngăn container Nginx thay đổi file cấu hình gốc trên máy Ubuntu, tăng cường tính toàn vẹn và bảo mật cho hệ thống.

#### Q8: Khi dùng Cloudflare Tunnel: có cần thiết phải mở cổng cho các service nữa không?
* **Trả lời:** **Không**. Tunnel tạo một đường kết nối từ bên trong máy ảo đi ra ngoài. Do đó, bạn có thể đóng toàn bộ port trên Router (80, 443, 1880), giúp hệ thống an toàn tuyệt đối trước các cuộc tấn công quét cổng từ Internet.
```
