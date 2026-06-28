Đây là một hệ thống cơ sở dữ liệu phân tán toàn cầu.

Bài toán: 
- Máy tính chỉ giao tiếp bằng địa chỉ IP.
- Nhưng con người nhớ địa ví dụ "google.com" "cloudflare.com"

Do đó cần hệ thống DNS, đây là hệ thống ánh xạ từ địa chỉ IP sang địa chỉ mà con người nhớ được.

### DNS có nhiều tầng
Root DNS  
↓  
TLD DNS  
↓  
Authoritative DNS

#### Root Server
Với 
```
google.com
```

Ví dụ hỏi IP của Google, Root sẽ không biết. Nhưng nó biết .com thì sẽ hỏi những sever nào.

#### TLD = Top Level Domain Server
TLD server biết google được quản lý bởi DNS nào. Ví dụ: 

```
google.com
      ↓
TLD .com
      ↓
Hỏi DNS của Google
```

#### Authoritative DNS
Đây mới là nơi có câu trả lời thật.

### Sâu hơn
Khi browser gửi request lên thanh tìm kiếm. Resolver là một máy chủ DNS nhận được yêu cầu. Nó sẽ tìm tới ROOT (là một máy chủ xác định, mapping các máy chủ khác). Sau đó lần theo TLD và Authoritative để tìm được DNS cần tìm.

.com  
.vn  
.net  
.org
Đây là các đuôi của máy chủ TLD, mỗi đuôi do một cụm máy chủ quản lý.

Root có danh sách
.com → DNS servers A,B,C  
.vn → DNS servers D,E,F  
.org → DNS servers G,H,I

Máy chủ Resolver cũng là xác định, ví dụ:
8.8.8.8 là Resolver của CloudFlare
1.1.1.1 là Resolver của Google

![[Pasted image 20260624163849.png]]

Các tên 
google.com  
facebook.com  
mycompany.com
được gọi là domain name (tên miền)

> Mỗi tầng chỉ biết tầng dưới nào chịu trách nhiệm, không cần biết dữ liệu cuối cùng.
Đó gọi là **delegation**.
