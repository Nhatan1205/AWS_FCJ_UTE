# Ngày 12: Elastic Compute Cloud (EC2)

Amazon EC2 là dịch vụ cung cấp máy chủ ảo (virtual server) trên nền tảng điện toán đám mây của AWS. Tương tự như việc thuê một máy chủ vật lý hoặc máy chủ ảo truyền thống, EC2 cho phép bạn nhanh chóng khởi tạo và chạy các máy chủ ảo với cấu hình linh hoạt. Điểm khác biệt lớn là AWS liên tục nâng cấp phần cứng, cung cấp các phiên bản mới mạnh mẽ hơn với chi phí tối ưu, giúp bạn dễ dàng mở rộng hoặc thu nhỏ tài nguyên theo nhu cầu (scalability).

EC2 phù hợp để triển khai nhiều loại workload như:

- Lưu trữ website, ứng dụng web
- Chạy các hệ quản trị cơ sở dữ liệu (CSDL)
- Các dịch vụ xác thực, xử lý backend
- Các công việc khác mà máy chủ vật lý hoặc máy chủ ảo truyền thống có thể đáp ứng

---

## Các loại cấu hình máy chủ (Instance Types)

Bạn không thể tùy ý cấu hình EC2, mà phải chọn **Instance Type** — một bộ cấu hình máy chủ ảo được AWS định nghĩa sẵn. Mỗi loại instance được thiết kế cho mục đích và hiệu năng khác nhau, quyết định các yếu tố quan trọng như:

- **CPU**: Số lượng và loại CPU (Intel là loại phổ biến nhất và thường có chi phí cao hơn, tiếp theo là AMD, còn ARM phổ biến cho các hệ điều hành Linux nhằm tối ưu hiệu suất và chi phí)
- **GPU**: Một số loại instance có tích hợp GPU chuyên dụng cho xử lý đồ họa hoặc AI/ML
- **Bộ nhớ (Memory)**: Dung lượng RAM phù hợp với nhu cầu tính toán
- **Mạng (Network)**: Băng thông và hiệu suất mạng, độ trễ
- **Lưu trữ (Storage)**: Loại và dung lượng ổ đĩa gắn kèm
- **Hardware Node**: Các instance được chạy trên phần cứng vật lý (hardware node). Bạn không thể chọn cụ thể phần cứng vật lý mà instance chạy trên đó, nhưng có thể cấu hình tùy chọn đặt (placement option) như:

  - Đặt nhiều EC2 instance trên cùng một hardware node để giảm độ trễ (latency)
  - Đặt các instance trên các hardware node khác nhau để tăng tính sẵn sàng (availability)

Trên mỗi hardware node, AWS sử dụng **hypervisor** để quản lý và phân phối tài nguyên phần cứng giữa các instance ảo. Hypervisor có các loại phổ biến như:

- **KVM** (Kernel-based Virtual Machine)
- **HVM** (Hardware Virtual Machine)
- **PV** (Paravirtualization)

Việc sử dụng loại hypervisor khác nhau cũng ảnh hưởng đến hiệu năng của instance.

---

## Amazon Machine Image (AMI), Backup và Key Pair

- **AMI (Amazon Machine Image)** là bản sao ảnh hệ điều hành và phần mềm cấu hình sẵn dùng để tạo EC2 instance. Một AMI bao gồm:

  - Root OS volume (ổ đĩa hệ điều hành)
  - Block device mapping (định nghĩa các ổ đĩa gắn kèm)
  - Quyền sử dụng (ai được phép dùng AMI)
  - Các phần mềm và cấu hình có sẵn

- Bạn có thể sử dụng:

  - AMI do AWS cung cấp sẵn
  - AMI mua từ **AWS Marketplace** (chợ ứng dụng)
  - AMI tùy chỉnh (custom AMI) do bạn tự tạo từ một instance EC2 đang chạy, giúp sao lưu hoặc triển khai nhiều máy chủ cùng cấu hình.

- **Backup EC2** thường được thực hiện bằng cách tạo **snapshot** từ ổ đĩa EBS (Elastic Block Store) gắn với instance. Snapshot giúp lưu lại trạng thái dữ liệu hiện tại để phục hồi khi cần.

- **Key Pair (cặp khóa)** gồm:

  - **Public key**: Được lưu trên instance EC2 để mã hóa dữ liệu đăng nhập
  - **Private key**: Người dùng giữ bí mật, dùng để giải mã và đăng nhập (ví dụ qua SSH)

Key Pair đảm bảo an toàn khi truy cập và quản lý EC2 instance.

---

## Một số điểm bổ sung quan trọng

- **Elasticity (tính co giãn):** Bạn có thể dễ dàng thay đổi số lượng instance chạy hoặc nâng cấp/downgrade instance type để phù hợp với nhu cầu thay đổi của ứng dụng.
- **Tính sẵn sàng và dự phòng:** EC2 tích hợp các vùng Availability Zone (AZ) cho phép đặt instance ở nhiều khu vực địa lý khác nhau nhằm đảm bảo tính dự phòng, tránh gián đoạn dịch vụ.
- **Tự động hóa:** EC2 có thể tích hợp với các dịch vụ khác của AWS như Auto Scaling, Elastic Load Balancing để tự động cân bằng tải và điều chỉnh tài nguyên.

---

Nếu bạn muốn, tôi có thể giúp bạn viết tiếp phần hướng dẫn sử dụng EC2 hoặc cung cấp các ví dụ thực tế về cách chọn instance type và quản lý AMI nhé!
