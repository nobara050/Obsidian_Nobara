Thứ tự thực thi:
Browser -> DNS -> TCP -> TLS -> HTTP -> Kestrel -> Middleware -> Controller

### DNS tìm IP của server
Khi nhập ví dụ api.myshop.com, máy tính không hiểu được tên miền. Nó cần địa chỉ IP ví dụ 203.0.113.10
Nên bước đầu tiên sẽ là: từ api.myshop.com -> DNS Query -> 203.0.113.10

### TCP thiết lập kết nối
Có IP rồi máy không gửi HTTP ngay mà sẽ phải tạo kết nối TCP trước.
TCP đảm bảo dữ liệu không mất, đúng thứ tự và kiểm tra lỗi.

Bắt đầu bằng 3 way handshake
- Client -> SYN
- Server -> SYN-ACK
- Client -> ACK
Sau bước này thì TCP sẽ connection established.

### TLS - mã hóa
Vì URL là "https://" nên cần TLS giúp mã hóa dữ liệu, xác thực server và chống nghe lén.

### HTTP 
HTTP Request sẽ có dạng 
Ví dụ:
GET /users/123 HTTP/1.1
Host: api.myshop.com
Accept: application/json

Server trả:
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id":123
}

### Kestrel
Kestrel là web server của ASP.NET Core

TCP Socket -> HTTP Parser -> ASP.NET Pipeline

### Middleware Pipeline
Request
   ↓
Authentication
   ↓
Authorization
   ↓
Controller

Hoặc có thêm tùy cấu hình

