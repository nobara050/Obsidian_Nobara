## RDS
AWS cung cấp dịch vụ **RDS**.
Nó là dịch vụ quản lý các database quen thuộc.

Ví dụ bạn chọn:

- MySQL
- PostgreSQL
- MariaDB

AWS sẽ lo:

- Cài đặt.
- Backup.
- Vá lỗi.
- Monitoring.
- Thay thế phần cứng khi cần.

Bạn chỉ quản lý dữ liệu và ứng dụng.

## Aurora

**Aurora** là database do AWS phát triển.

Điểm cần nhớ:
- Tương thích MySQL và PostgreSQL.
- Hiệu năng cao hơn RDS thông thường.
- Tự động sao chép dữ liệu trên nhiều AZ.
- Được AWS tối ưu riêng cho Cloud.

Nếu đề hỏi:
> "Cần database quan hệ hiệu năng cao trên AWS."

→ Aurora thường là đáp án.

## Amazon DynamoDB

Dịch vụ NoSQL nổi tiếng nhất của AWS.

Đặc điểm:

- Serverless.
- Scale gần như không giới hạn.
- Độ trễ rất thấp (single-digit milliseconds).

AWS quản lý toàn bộ hạ tầng.

Bạn không cần quan tâm:

- Server.
- Ổ cứng.
- Replication.

## Database Migration

**AWS Database Migration Service (DMS)**

Mục đích chuyển database từ:
- On-premises
- Database khác
- Cloud khác
sang AWS.

Điểm quan trọng:
AWS cố gắng giảm thời gian gián đoạn (downtime) khi di chuyển dữ liệu.

## Bảng cần thuộc

|Dịch vụ|Dùng để làm gì|
|---|---|
|Amazon RDS|Database quan hệ được AWS quản lý|
|Amazon Aurora|Database quan hệ hiệu năng cao, tương thích MySQL/PostgreSQL|
|Amazon DynamoDB|NoSQL, Serverless, quy mô lớn|
|AWS DMS|Di chuyển database sang AWS|
