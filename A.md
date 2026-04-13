# Phần A: Đăng ký tên miền cá nhân và Cấu hình Cloudflare
## 1. Đăng ký tên miền cá nhân
Em đã tiến hành đăng ký thành công tên miền cá nhân
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bbb6b2a4-b9d5-4719-bc30-e43ad4f93d4c" />

## 2. Khởi tạo tài khoản Cloudflare
Tiến hành tạo tài khoản Cloudflare để sử dụng dịch vụ quản lý DNS và bảo vệ proxy.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/557b30da-e4d6-48d0-b167-09f344300562" />
## 3. Thêm Domain vào Cloudflare và lấy Nameserver
Em đã thêm tên miền vừa đăng ký vào hệ thống của Cloudflare (sử dụng gói Free). Cloudflare đã cấp phát 2 địa chỉ Nameserver để thực hiện việc ủy quyền quản lý DNS.
<img width="1920" height="1080" alt="Ảnh chụp màn hình (710)" src="https://github.com/user-attachments/assets/f63fd547-7f2a-4b6a-84e2-bf66b9cfd886" />
## 4. Trỏ Nameserver về Cloudflare
Để Cloudflare có quyền quản lý luồng traffic và các bản ghi DNS của tên miền, em đã quay lại trang quản lý của nhà cung cấp tên miền để thay đổi Nameserver mặc định sang Nameserver của Cloudflare.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2027853c-935f-4160-9e91-ba5d101d1b80" />
Sau một thời gian chờ DNS cập nhật (propagate), Cloudflare đã nhận diện thành công tên miền và báo trạng thái **Active**. Từ thời điểm này, mọi cấu hình trỏ IP hoặc tạo Tunnel (Sub-domain) sẽ được thực hiện hoàn toàn trên Cloudflare.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b74c93dd-5031-4402-843d-a22d5d40cbcf" />
