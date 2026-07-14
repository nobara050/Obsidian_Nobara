[[Microservice]]

**Đúng** Microservice là chia hệ thống thành nhiều service độc lập theo nghiệp vụ.
Microservice được chia theo **nghiệp vụ**, không phải theo tầng kỹ thuật.
**Sai Microservice là việc chia project thành nhiều project.**

**Mỗi lần sửa Payment phải deploy toàn bộ. Đây là micro hay mono?** 
=> Monolith

Microservice thường hướng tới **Stateless**.

**Bounded Context** dùng để mô tả ranh giới nghiệp vụ nơi một mô hình domain có ý nghĩa nhất quán.

**Availability** hệ thống có sẵn sàng phục vụ hay không.

**Fraut Tolerance** giúp hệ thống tiếp tục hoạt động khi một thành phần gặp lỗi.

RabbitMQ góp phần tăng đặc tính nào của Microservice? => **Loose Coupling**

Trong Microservice, mỗi service nên chịu trách nhiệm cho **Một Bussiness Capability**

**Stateless Service** Không lưu trạng thái trong memory.

Ưu điểm của Stateless là **Dễ Scale**

Session lưu trong RAM của server là **Stateful**

**Scale out là Horizontal Scaling**

**Scale up là tăng CPU hoặc RAM**

Khi nào nên **Horizontal Scaling**: muốn phục vụ nhiều request hơn.

**Reliability** hệ thống hoạt động đúng và ổn định.

**Resilience** khả năng phục hồi sau lỗi.

# API Gateway
> Single Entry Point của toàn bộ hệ thống.

## Nhiệm vụ của API Gateway

- Routing: chức năng quan trọng nhất.
- Authentication: kiểm tra JWT có hợp lệ không.
- Authorization: kiểm tra Role.
- SSL Termination: gateway xử lý TLS và SSL Certificate.
- Rate Limiting: Ngăn spam.
- Load Balancing: gateway có thể chọn xử lý request nào. Các thuật toán: Round Robin, Least Connection, IP Hash.
- Aggregation: giúp gộp nhiều response.
- Caching: lưu các kết quả hay được đùng lại để giảm tải server.
- Logging
- Monitoring

## Không nên làm: 

- Xử lý business logic.
- Truy cập database.
- Validate nghiệp vụ.

# Reverse Proxy và Forward Proxy

**Reverse Proxy và Forward Proxy** đều là các máy chủ trung gian (proxy server) nằm giữa client và server, nhưng chúng khác nhau ở đối tượng mà chúng đại diện.

**Forward Proxy** đại diện cho **client**. Khi client muốn truy cập Internet, request sẽ được gửi đến Forward Proxy trước, sau đó Proxy mới gửi request đến server đích. Đối với server, request dường như đến từ Proxy chứ không phải từ client thật. Vì vậy, Forward Proxy thường được sử dụng để kiểm soát việc truy cập Internet, ẩn địa chỉ IP của client, lọc nội dung, cache dữ liệu hoặc vượt qua một số giới hạn về mạng. Ví dụ, trong mạng nội bộ của một công ty, tất cả nhân viên có thể bắt buộc phải truy cập Internet thông qua một Forward Proxy để công ty có thể chặn một số website hoặc ghi lại lịch sử truy cập.

**Reverse Proxy** lại đại diện cho **server**. Client không kết nối trực tiếp đến các backend server mà chỉ biết đến một địa chỉ duy nhất của Reverse Proxy. Sau khi nhận request, Reverse Proxy sẽ dựa vào các quy tắc định tuyến (routing rules) để chuyển tiếp request đến backend service phù hợp. Trong Microservice, việc định tuyến thường dựa trên **Path** của URL, ví dụ `/orders` sẽ được chuyển đến Order Service, còn `/users` sẽ được chuyển đến User Service. Đối với client, toàn bộ hệ thống chỉ có một endpoint duy nhất, trong khi vị trí, địa chỉ IP hoặc Port của các backend service đều được ẩn đi.

# Service Discovery

|Keyword|Ý nghĩa|
|---|---|
|Service Discovery|Tìm vị trí của service|
|Service Registry|Nơi lưu danh sách service|
|Service Registration|Service tự đăng ký khi khởi động|
|Static Routing|Gateway cấu hình IP/Port cố định|
|Dynamic Routing|Gateway hỏi Registry để lấy địa chỉ|
|Health Check|Kiểm tra service còn hoạt động|
|Heartbeat|Tín hiệu định kỳ báo service còn sống|
|Client-side Discovery|Client hỏi Registry|
|Server-side Discovery|Gateway/Load Balancer hỏi Registry|

> **Static Routing** là cách API Gateway hoặc Reverse Proxy được cấu hình cố định địa chỉ IP và Port của từng service. Khi một service thay đổi IP hoặc Port, nhà phát triển phải cập nhật lại cấu hình và triển khai lại Gateway. Cách này đơn giản nhưng không phù hợp với hệ thống có nhiều service hoặc thường xuyên scale.

> **Dynamic Routing** là cách API Gateway không lưu trực tiếp IP và Port của service. Thay vào đó, Gateway sử dụng **Service Discovery** để tìm địa chỉ của service tại thời điểm xử lý request. Mỗi service khi khởi động sẽ thực hiện **Service Registration** để đăng ký thông tin của mình vào **Service Registry**. Registry lưu tên service, địa chỉ IP, Port và trạng thái hoạt động của các instance. Khi Gateway cần gọi một service, nó sẽ hỏi Registry để lấy địa chỉ mới nhất rồi mới chuyển tiếp request.

# Docker

Image là một **mẫu (template)** chứa mọi thứ cần để chạy ứng dụng.

Muốn chạy Image, docker tạo Contrainer. Container mới là tiến trình đang chạy.

Bạn có

```
sqlserver-image
```

Bạn chạy

```
docker run sqlserver-image
```

↓

Có

```
SQL Server Container
```

đang chạy.

## Mối quan hệ
Một image có nhiều Container

## Docker Engine
Không phải OS chạy Container mà là Docker Engine

## Docker CLI
CLI gửi yêu cầu cho Docker Engine.

```
Bạn  
  
↓  
  
docker run  
  
↓  
  
Docker CLI  
  
↓  
  
Docker Engine  
  
↓  
  
Image  
  
↓  
  
Container
```

## Volume

Nơi lưu trữ dữ liệu bên ngoài Container.

Dùng khi dữ liệu cần tồn tại lâu dài:

- Database
- File upload
- Log
- Storage

Không dùng Volume cho:

- Source code tạm
- File build tạm

## Docker Network

Bạn có:

```
id="m7v4hu"
Order Service
localhost:5000
	↓
RabbitMQ
localhost:5672
```

Bạn chạy Order Service trong Container.

Nó gọi:

```
localhost:5672
```

Lỗi.

Tại sao?

Vì trong Container:

`localhost` nghĩa là:

> Chính Container đó

Không phải máy của bạn.

=> Docker Network giúp các Container giao tiếp với nhau.

Khi nhiều container cần giao tiếp:

- API gọi API
- API gọi Database
- API gọi RabbitMQ
- API gọi Redis

Trong Microservice gần như luôn dùng.

## Docker Compose

Project có:

```
id="z6x81n"
Gateway
User API
Order API
SQL Server
RedisRabbitMQ
```

Nếu chạy từng cái:

```
docker run user-api
docker run order-api
docker run sql
docker run redis
docker run rabbitmq
```

Rất dài.

Docker Compose cho phép định nghĩa nhiều Container trong một file.
docker-compose.yml

```
services:  
  
api:  
image: ecommerce-api  
  
sql:  
image: sqlserver  
  
rabbitmq:  
image: rabbitmq
```

Compose tự tạo Network

## Dockerfile
Dockerfile là file chứa các bước để Docker tạo Image.

# Azure
Azure là một nền tảng cloud cung cấp các dịch vụ để triển khai, lưu trữ và quản lý ứng dụng.

Khi làm việc với Azure, mọi thành phần được quản lý dưới dạng **Resource**. Resource là một tài nguyên cụ thể như Database, Storage, Virtual Machine, App Service hoặc Container. 

Các Resource được tổ chức bên trong **Resource Group**, là một nhóm logic giúp quản lý, phân quyền và theo dõi các tài nguyên của cùng một ứng dụng hoặc môi trường. 

Các Resource Group nằm trong **Subscription**, nơi quản lý billing, quyền truy cập và phạm vi tài nguyên của một tổ chức.

Mỗi Resource được triển khai trong một **Region**, là vị trí địa lý của Azure Data Center. Việc chọn Region ảnh hưởng đến latency, chi phí và khả năng đáp ứng yêu cầu hệ thống. Một Region có thể có nhiều **Availability Zone**, là các khu vực Data Center độc lập giúp tăng tính sẵn sàng. Khi một Zone gặp sự cố, ứng dụng có thể tiếp tục hoạt động ở Zone khác.

Azure CLI là công cụ dòng lệnh để quản lý Azure thay vì thao tác bằng Portal. Người dùng sử dụng `az login` để xác thực với Azure, sau đó có thể tạo và quản lý tài nguyên bằng command. Ví dụ `az group create` dùng để tạo Resource Group. Azure CLI thường được dùng trong CI/CD pipeline vì có thể tự động hóa quá trình deploy.

Trong quá trình triển khai ứng dụng Docker, Azure sử dụng **Azure Container Registry (ACR)** để lưu trữ Docker Image. Sau khi developer build image bằng Docker, image được tag theo format của ACR rồi push lên registry. ACR không chạy application mà chỉ đóng vai trò nơi lưu trữ image, tương tự như Docker Hub. Sau đó các dịch vụ chạy container trên Azure sẽ lấy image từ ACR để triển khai.

Flow triển khai Docker lên Azure thường là:

```
Source Code  
|  
v  
docker build  
|  
v  
Docker Image  
|  
v  
Push lên Azure Container Registry  
|  
v  
Azure Container Apps / App Service / VM  
|  
v  
Application chạy
```

Azure cung cấp nhiều lựa chọn để deploy ứng dụng. **Azure App Service** là dịch vụ PaaS, phù hợp khi muốn deploy ứng dụng nhanh mà không cần quản lý server. Azure chịu trách nhiệm về hệ điều hành, runtime, scaling cơ bản và infrastructure. Ví dụ một ASP.NET Core API đơn giản có thể deploy trực tiếp lên App Service.

**Azure Container Apps** phù hợp hơn với ứng dụng được đóng gói bằng Docker Container, đặc biệt là kiến trúc Microservice. Container Apps nhận Docker Image từ ACR và chạy container, đồng thời hỗ trợ scaling và quản lý nhiều service. Trong hệ thống Microservice có nhiều API như User Service, Order Service, Payment Service, Container Apps thường là lựa chọn phù hợp hơn App Service.

**Azure Virtual Machine (VM)** là máy chủ ảo trên cloud. VM cho phép toàn quyền quản lý hệ điều hành, cài đặt phần mềm và cấu hình server. Tuy nhiên người dùng phải tự quản lý nhiều thứ hơn như patch, security, scaling. VM phù hợp khi cần quyền kiểm soát cao hoặc chạy hệ thống đặc biệt.

Sự khác nhau chính giữa các lựa chọn deploy là mức độ quản lý. App Service và Container Apps thuộc nhóm Azure quản lý nhiều hơn, giúp developer tập trung vào application. VM cho phép kiểm soát nhiều hơn nhưng cần nhiều công việc vận hành hơn.

## IaaS — Infrastructure as a Service

Bạn thuê **hạ tầng**.

Azure cung cấp:

- Máy chủ ảo (VM)
- CPU
- RAM
- Disk
- Network

Nhưng bạn tự quản lý phần bên trên.

## PaaS — Platform as a Service

Bạn thuê **môi trường chạy ứng dụng**.

Azure quản lý thêm nhiều thứ.

Azure lo:

```
Hardware
OS
Runtime
Web Server
Scaling cơ bản
```

Bạn chỉ lo:

```
Code
Configuration
Data
```

## SaaS — Software as a Service

Bạn chỉ dùng **phần mềm hoàn chỉnh**.

Bạn không quản lý gì về hệ thống.