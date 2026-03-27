# Observability Stack: Metrics & Logging

Dự án triển khai hệ thống giám sát toàn diện (Monitoring & Logging) sử dụng Docker Compose. Hệ thống thu thập số liệu (Metrics) và nhật ký (Logs), sau đó trực quan hóa trên một giao diện duy nhất.


##  Kiến trúc Hệ thống

Dự án được chia thành 2 khối chính:

### 1. Khối Metrics (Giám sát chỉ số)
* **Prometheus:** Thu thập số liệu từ các target.
* **VictoriaMetrics:** Giải pháp lưu trữ Time-Series Database (TSDB) tối ưu dung lượng, hiệu năng cao thay thế cho bộ lưu trữ mặc định.
* **Node Exporter:** Agent thu thập thông số phần cứng (CPU, RAM, Disk) của máy chủ Linux.
* **Alertmanager & vmalert:** Xử lý và gửi cảnh báo (Telegram/Slack/Email).

### 2. Khối Logs (Quản lý nhật ký tập trung)
* **Loki (Microservice Architecture):** Triển khai theo mô hình Simple Scalable (tách biệt Gateway, Read, Write, Backend) sử dụng 100% Local Filesystem và TSDB index (Không dùng S3).
* **Promtail:** Agent đọc file log hệ thống (`/var/log/syslog`) và đẩy lên Gateway.

### 3. Giao diện (Visualization)
* **Grafana:** Bảng điều khiển trung tâm, kết nối đồng thời với khối Metrics và khối Logs.

## Hướng dẫn cài đặt & Khởi chạy

**Yêu cầu môi trường:** Docker và Docker Compose.

1. **Clone repository:**
   ```bash
   git clone https://github.com/Teinsky/Observability-Stack
   cd observability-stack
