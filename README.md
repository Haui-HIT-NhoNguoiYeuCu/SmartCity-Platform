# SmartCity-Platform (Bài dự thi PMNM 2025)

**Đội:** [Tên Đội Của Bạn]
**Trường:** [Tên Trường Của Bạn]

Bài dự thi Xây dựng ứng dụng thành phố thông minh dựa trên nền tảng dữ liệu mở.

## 💡 Ý tưởng cốt lõi

Dự án này xây dựng một **Nền tảng Dữ liệu Đô thị** (Urban Data Platform) có khả năng phục hồi cao, giải quyết vấn đề quá tải (ingestion overhead) trong Smart City.

Thay vì PUSH dữ liệu trực tiếp, kiến trúc của chúng tôi sử dụng mô hình **Edge Storage (Buffer)** và **Smart Agent (Pull)** với logic ưu tiên:

1.  **Dữ liệu Nóng (Hot):** (Cảnh báo tức thời) - Được ưu tiên PULL và xử lý ngay (delay tính bằng giây).
2.  **Dữ liệu Ấm (Warm):** (Phân tích hàng ngày) - PULL với độ trễ chấp nhận được (delay tính bằng ngày).
3.  **Dữ liệu Lạnh (Cold):** (Lưu trữ dài hạn) - PULL khi hệ thống rảnh rỗi.

Nền tảng này tuân thủ 100% yêu cầu kỹ thuật của đề bài (NGSI-LD, FIWARE Models) và đóng vai trò là hạ tầng cho ứng dụng "GreenX" (Demo Cảnh báo Ô nhiễm & Cây xanh).

## 🏗️ Kiến trúc Hệ thống
## 🛠️ Công nghệ & Phụ thuộc 

Nền tảng này sử dụng và tích hợp các PMMN sau:

* **Context Broker (Lớp Nóng):** FIWARE Orion-LD
* **Edge Storage (Buffer):** NATS.io (hoặc RabbitMQ)
* **Historical (Lớp Ấm):** TimescaleDB
* **Storage (Lớp Lạnh):** MinIO
* **Smart Agent (Logic Pull):** Spring Boot 3 (Java)
* **Đóng gói & Vận hành:** Docker & Docker Compose

## 🚀 Hướng dẫn Cài đặt 

Hệ thống yêu cầu đã cài đặt **Docker** và **Docker Compose**.

1.  **Clone kho mã nguồn:**
    ```bash
    git clone https://github.com/Haui-HIT-NhoNguoiYeuCu/SmartCity-Platform.git
    ```

2.  **Di chuyển vào thư mục dự án:**
    ```bash
    cd SmartCity-Platform
    ```

3.  **Biên dịch và khởi chạy toàn bộ nền tảng:**
    (Lệnh này sẽ tự động build Smart Agent và khởi chạy mọi dịch vụ)
    ```bash
    docker-compose up -d --build
    ```

4.  **Xem Giao diện Web (Ví dụ):**
    * **Giao diện GreenX (Demo):** `http://localhost:80`
    * **MinIO (Lớp Lạnh):** `http://localhost:9001`
    * **NATS Monitor:** `http://localhost:8222`

5.  **Dừng hệ thống:**
    ```bash
    docker-compose down
    ```