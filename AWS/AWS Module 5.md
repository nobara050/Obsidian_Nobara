**Region**: Khu vực địa lý 

**Availability Zone**: một region có nhiều Availability Zone, chứa một hoặc nhiều Data Center

Các AZ được kết nối mạng tốc độ cao với nhau.

**Amazon VPC** là **mạng riêng của bạn trên AWS**.
Một VPC có thể có nhiều **Subnet**
- Một Subnet chỉ thuộc **một AZ**.
- Một AZ có thể có nhiều Subnet.

**Public Subnet** dùng cho các tài nguyên cần được truy cập từ Internet.
Thường chứa:
- Load Balancer
- Web Server
- Bastion Host

**Private Subnet** không cho Internet truy cập trực tiếp.
Thường chứa:
- Database
- Redis
- Backend nội bộ

Security Group là **Firewall ở cấp tài nguyên**.
Nó quyết định:
- Ai được truy cập?
- Qua cổng (Port) nào?
**Đặc điểm:**
- Stateful.
- Chỉ có **Allow**.
- Gắn vào EC2, RDS, ALB...

NACL là **Firewall ở cấp Subnet**.
Đặc điểm:
- Stateless.
- Có **Allow** và **Deny**.

Site-to-Site VPN dùng kết nối qua internet công khai (IPsec) nên chi phí thấp hơn nhiều so với Direct Connect

Client VPN được thiết kế riêng cho việc kết nối từ thiết bị cá nhân (client) đến VPC, hỗ trợ tích hợp xác thực như Active Directory, SAML, mutual authentication, và có thể scale nhanh cho nhiều người dùng

Internet gateway chỉ cho phép VPC truy cập internet công khai

Virtual private gateway là thành phần phía AWS dùng cho VPN (qua internet, không phải dedicated)

CloudFront là dịch vụ CDN, không liên quan đến kết nối network
