# DAY 05: AWS Virtual Private Cloud (VPC)

## Amazon Virtual Private Cloud (VPC)
Amazon VPC cung cấp một môi trường mạng ảo riêng biệt, giúp các doanh nghiệp xây dựng và quản lý môi trường mạng ảo hóa cho các dịch vụ công cộng và kết nối với cơ sở hạ tầng nội bộ (on-premise). Với VPC, bạn có thể khởi chạy tài nguyên AWS trong một mạng ảo được xác định rõ ràng, với địa chỉ IP riêng biệt cho mỗi tài nguyên.

### Tính Chất của VPC:

- **Vị trí trong Region:** VPC nằm trong một vùng AWS Region và phải được cấu hình với địa chỉ IPv4, đồng thời hỗ trợ IPv6.
- **Giới hạn:** Một tài khoản AWS có thể có tối đa 5 VPC trong mỗi Region.
- **Mục đích phân tách môi trường:** VPC giúp phân tách các môi trường khác nhau như phát triển (dev), kiểm thử (test), sản xuất (prod), giúp quản lý tài nguyên dễ dàng hơn.
- **Mạng cô lập:** Các VPC hoạt động độc lập và cô lập ở cấp độ mạng, giúp bảo mật và quản lý lưu lượng truy cập hiệu quả.

### Subnet (Mạng con):
VPC cho phép bạn chia mạng ảo thành các **subnet** (mạng con), giúp quản lý và phân phối tài nguyên dễ dàng hơn. Mỗi subnet sẽ nằm trong một **Availability Zone (AZ)** cụ thể. Khi tạo subnet, bạn cần chỉ định một CIDR block cho subnet đó. AWS sẽ giữ lại 5 địa chỉ IP đầu tiên và cuối cùng trong mỗi subnet, và bạn không thể gán chúng cho các máy chủ.

### Kiến Trúc Của VPC:

- **Route Table:**  
  Route Table chứa các bảng định tuyến để xác định đường đi của các gói dữ liệu trong mạng. Khi tạo một VPC, AWS tự động tạo một **default route table**, cho phép tất cả các subnet có thể giao tiếp với nhau. Bạn có thể tạo **custom route tables** để định tuyến lưu lượng ra ngoài internet hoặc giữa các subnet khác nhau trong VPC.

- **Elastic Network Interface (ENI):**  
  **ENI** là một card mạng ảo gắn với mỗi máy chủ EC2. Mỗi ENI có một hoặc nhiều địa chỉ IP và có thể được gán vào nhiều máy chủ khác nhau mà không làm thay đổi địa chỉ IP.

- **Elastic IP Address (EIP):**  
  **EIP** là địa chỉ IP công cộng tĩnh, có thể gắn vào một ENI và được sử dụng để duy trì kết nối mạng bền vững. Tuy nhiên, lưu ý rằng sử dụng EIP sẽ bị tính phí nếu không được liên kết với một EC2 instance.

### Các Thành Phần Khác trong Kiến Trúc VPC:

- **VPC Endpoint:**  
  **VPC endpoint** cho phép kết nối tài nguyên trong VPC với các dịch vụ AWS được hỗ trợ, như S3 và DynamoDB, mà không cần phải ra ngoài internet.
  
  - **Interface Endpoint:** Sử dụng ENI trong VPC với địa chỉ private để kết nối tới dịch vụ hỗ trợ.
  - **Gateway Endpoint:** Định tuyến lưu lượng thông qua route table tới các dịch vụ hỗ trợ như S3 và DynamoDB.

- **Internet Gateway:**  
  **Internet Gateway** là thành phần mở rộng có khả năng mở rộng quy mô theo chiều ngang, cho phép các EC2 instance trong VPC có thể truyền thông tin ra ngoài internet. Đây là cầu nối giữa VPC và internet.

- **NAT Gateway:**  
  **NAT Gateway** cho phép các EC2 instance trong private subnet có thể truy cập internet hoặc các dịch vụ AWS khác. Tuy nhiên, NAT Gateway chỉ cho phép kết nối đi một chiều (outbound) mà không cho phép kết nối quay lại (inbound).

### Tóm Tắt Kiến Trúc Mới:
VPC là nền tảng mạnh mẽ giúp bạn quản lý tài nguyên AWS một cách linh hoạt và bảo mật. Các tính năng như Route Table, ENI, EIP, VPC Endpoint, Internet Gateway, và NAT Gateway giúp tối ưu hóa kết nối giữa các tài nguyên trong VPC và các dịch vụ AWS khác, đồng thời cung cấp khả năng bảo mật và kiểm soát lưu lượng dữ liệu.

Với VPC, bạn có thể dễ dàng phân chia các môi trường phát triển, kiểm thử và sản xuất, và đảm bảo rằng dữ liệu và tài nguyên của mình được bảo vệ trong một môi trường mạng ảo được kiểm soát.
