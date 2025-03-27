# Bản tóm tắt ngắn gọn hơn về Kubernetes

## Kubernetes là gì và tại sao nó quan trọng? (5%)

### Định nghĩa

- Kubernetes là một nền tảng mã nguồn mở để tự động hóa việc triển khai, mở rộng và quản lý các ứng dụng chứa (containerized applications). Nó được thiết kế để xử lý các hệ thống phân tán phức tạp.

### Tại sao cần Kubernetes?

- Giải quyết vấn đề quản lý hàng trăm/thousands container trên nhiều máy chủ.
- Đảm bảo ứng dụng luôn chạy ổn định (high availability), tự động scale theo tải, và phục hồi khi có lỗi (self-healing).

### Ý tưởng cốt lõi

- Bạn không quản lý từng container riêng lẻ mà giao phó cho Kubernetes tự động điều phối dựa trên các khai báo (declarative configuration).

## Kiến trúc cơ bản của Kubernetes (10%)

- **Cluster**: Một cụm Kubernetes gồm Master Node (điều khiển) và Worker Node (chạy ứng dụng).
  - **Master Node**: Chứa các thành phần quản lý
    - **API Server**: "Bộ não" nhận lệnh từ người dùng (qua kubectl) và điều phối cluster.
    - **Controller Manager**: Theo dõi trạng thái cluster, đảm bảo trạng thái thực tế khớp với trạng thái mong muốn.
    - **Scheduler**: Quyết định container chạy trên node nào dựa trên tài nguyên và yêu cầu.
    - **etcd**: Cơ sở dữ liệu lưu trữ trạng thái của cluster.
  - **Worker Node**: Chạy ứng dụng thực tế:
    - **Kubelet**: Đại diện của Kubernetes trên mỗi node, thực thi lệnh từ Master.
    - **Kube-Proxy**: Quản lý mạng, định tuyến traffic giữa các container.
    - **Container Runtime (như Docker)**: Chạy các container thực sự.
- Nguyên lý hoạt động: Master quản lý, Worker thực thi. Tất cả giao tiếp qua API Server.

## Cách Kubernetes vận hành ứng dụng (5%)

### Automation

- **Self-Healing**: Pod chết -> Kubernetes tự tạo Pod mới thay thế.
- **Auto-Scaling**: Tăng/giảm số Pod dựa trên tải (CPU, memory) qua Horizontal Pod AutoScaler (HPA).

### Deployment

- Dùng file YAML để khai báo (ví dụ: số bản sao, image container, port).
- Lệnh `kubectl apply -f file.yaml` để áp dụng.

### Network

- Mỗi Pod có IP riêng, Service định tuyến traffic. Kubernetes dùng CNI (Container Network Interface) như Flannel, Calico để quản lý mạng.
