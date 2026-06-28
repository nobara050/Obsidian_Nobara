TCP nhận trách nhiệm vận chuyển byte từ máy này sang máy khác.
- Thiết lập kết nối,
- Truyền dữ liệu.
- Đảm bảo dữ liệu không mất.
- Đảm bảo dữ liệu đúng thứ tự.

## Kết nối TCP
Trước khi gửi dữ liệu client thiết tập kết nối với server.
Đây gọi là three-way handshake

```
1. Client gửi tới Server packat SYN
2. Server gửi lại cho Client packet SYN + ACK
3. Client gửi lại packet ACK
```

Bên trong packet SYN chứa Sequence Number.
Ví dụ Client gửi Seq = 1000.

Sequence Number ở đây là số thứ tự của byte trong luồng dữ liệu TCP.
```
H e l l o   W o r l  d  
1 2 3 4 5 6 7 8 9 10 11
```
Sequence Number được dùng để biết byte nào đã nhận, byte nào thiếu và cần gửi lại.

Khi gửi seq 1000 tức là Byte đầu tiên mà Client sẽ gửi trong kết nối này sẽ bắt đầu từ vị trí 1000.

Server nhận được và trả SYN + ACK về cho Client
```
Seq = 5000
Ack = 1001
```
Ý nghĩa là Byte đầu tiên Server gửi sẽ bắt đầu từ 5000.
ACK 1001 nghĩa là server đã nhận seq 1000 và mong đợi nhận tiếp là 1001.

Client sau khi nhận được cũng sẽ trả lại 
```
Seq = 1001
Ack = 5001
```
Nghĩa là đã nhận được SYN của Server có seq là 5000.
Mong đợi nhận tiếp theo là 5001.

## Sâu hơn
TCP không gửi từng byte riêng lẻ mà thường gửi theo segment (gói TCP).
Ví dụ 
```
Packet A
Seq = 1001
Length =2
```
Chứa byte 1001 và byte 1002

```
Packet B
Seq = 1003
Length = 2
```
Chứa byte 1003, 1004

```
Packet C
Seq = 1005
Length = 1
```
Chứa byte 1005

Giả sử Client gửi cho Server 3 packet trên và packet B bị mất:
Server nhận được 1001 và 1002
Sau đó đột nhiên 1005 => thấy thiếu 1003 và 1004.
Server sẽ gửi Ack = 1003.

Client vẫn tiếp tục gửi 1006, 1007, 1008,... nhưng thấy Ack = 1003 lặp lại liên tục => duplicate Ack.

Khi nhận đủ 3 duplicate Ack thì Client kết luận byte 1003 bị mất và gửi lại 1003, 1004. Nếu không cần đợi timeout thì gọi là Fast Retrainsmit.

==Vấn đề:==  Nếu 1003 là packet cuối, nó sẽ không gửi Ack 1005 được và cũng không gửi duplicate được. Nó sẽ Retransmission Timeout (RTO). Tức là gửi lại sau khi timeout.

```
RTO ≈ RTT × hệ số an toàn
```

Nó sẽ tính thời gian Round Trip Time (RTT)
Tức là một lần 
```
Client
 ↓
Server
 ↓
Client
```

