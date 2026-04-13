# Phần E: Triển khai và Kiểm thử ứng dụng

Em đã thực hiện tích hợp giữa giao diện Web (Nginx) và dịch vụ xử lý (Node-RED) để kiểm tra luồng dữ liệu.

## 1. Thiết lập API trên Node-RED
Em đã tạo một endpoint GET `/test-api` trên Node-RED để trả về dữ liệu định dạng JSON. Điều này giả lập một dịch vụ cung cấp dữ liệu từ các thiết bị IOT.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/73aa853b-75de-49ab-b148-a10f4f55e028" />

## 2. Kiểm thử Reverse Proxy
Bằng cách sử dụng Javascript Fetch trên trang `index.html`, em đã gọi đến địa chỉ `/api/test-api`. Nginx đã nhận yêu cầu tại cổng 80 và điều hướng chính xác vào dịch vụ Node-RED nội bộ.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d82d27a7-3098-47d4-b5d5-756bd8a1dcac" />
