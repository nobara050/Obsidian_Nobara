A **Microservice Architecture** is an architectural style where an application is split into many **small independent services**.

Each service:
- has one responsibility
- has its own business logic
- can be deployed independently
- usually owns its own database
- communicates with other services

**Quiz keyword**
> Independent Deployment

# Why Microservice?

Advantages
- Independent deployment
- Easier scaling
- Smaller codebase
- Fault isolation
- Different teams can work independently
- Different technologies can be used

Disadvantages
- More complex
- Hard debugging
- Network latency
- Distributed transactions
- Monitoring becomes harder

# Monolith vs Microservice

| Monolith                  | Microservice              |
| ------------------------- | ------------------------- |
| One application           | Many applications         |
| One deployment            | Independent deployment    |
| Usually one database      | Database per service      |
| Easy to develop initially | Harder initially          |
| Hard to scale partially   | Scale only needed service |
| Tight coupling            | Loose coupling            |

# gRPC

Instead of JSON
Uses

```
Protocol Buffers
```

**Advantages**
- Faster
- Smaller payload
- Better performance

**Disadvantages**
- Harder to debug.
- Keyword
- Protocol Buffers (protobuf)

# Message Broker

**Purpose**
Deliver messages between services.

**Popular**
- RabbitMQ
- Kafka
- Azure Service Bus
- ActiveMQ

**Message Broker provides**
- asynchronous communication
- decoupling
- retry
- buffering

# CI - Continuous Integration

Automatically verify every code change.

**Typical flow:**

```
Developer    
	|
Git Push    
	|
Repository (GitHub/Azure DevOps)    
	|
CI Pipeline    
	|
Restore packages    
	|
Build    
	|
Run Unit Tests    
	|
Publish Build Artifact
```

Imagine you commit this:

```
git commit
git push
```

Immediately the CI server starts.

**It will usually:**
1. Download source code
2. Restore NuGet packages
3. Compile
4. Run unit tests
5. Check code quality (optional)
6. Produce build artifacts

**Keyword**
```
dotnet publish
```
creates the artifact

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

Reverse Proxy mang lại nhiều lợi ích cho hệ thống. Nó giúp che giấu hạ tầng phía sau, giảm sự phụ thuộc của client vào địa chỉ IP và Port của từng service, đồng thời hỗ trợ các tính năng như Load Balancing, SSL/TLS Termination, URL Rewrite, Compression, Caching và Logging. Khi một service thay đổi IP hoặc Port, chỉ cần cập nhật cấu hình của Reverse Proxy mà không cần sửa ứng dụng phía client.

Một điểm quan trọng cần phân biệt là **Forward** và **Redirect**. Khi Reverse Proxy **forward** request, client hoàn toàn không biết request đã được chuyển sang backend nào vì toàn bộ quá trình diễn ra bên trong hệ thống. Ngược lại, **Redirect** là khi server trả về mã trạng thái HTTP như `301` hoặc `302`, yêu cầu browser gửi một request mới đến địa chỉ khác, vì vậy client biết mình đang được chuyển sang một URL mới.

Trong kiến trúc Microservice, **API Gateway** thường được xây dựng dựa trên **Reverse Proxy**. Reverse Proxy chịu trách nhiệm nhận và chuyển tiếp request, còn API Gateway mở rộng thêm nhiều chức năng như Authentication, Authorization, Rate Limiting, Request Aggregation, Logging và Monitoring. Có thể hiểu rằng **mọi API Gateway đều hoạt động như một Reverse Proxy, nhưng không phải mọi Reverse Proxy đều là API Gateway**. Trong hệ sinh thái .NET, **YARP (Yet Another Reverse Proxy)** là một Reverse Proxy do Microsoft phát triển và có thể mở rộng để trở thành API Gateway, trong khi **Ocelot** được thiết kế ngay từ đầu như một API Gateway hoàn chỉnh dành cho ASP.NET Core.



