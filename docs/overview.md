# Tổng quan RabbitMQ
---
## Tổng quan
### RabbitMQ
RabbitMQ là một message broker ( message-oriented middleware) sử dụng giao thức AMQP - Advanced Message Queue Protocol (Đây là giao thức phổ biến, thực tế rabbitmq hỗ trợ nhiều giao thức). RabbitMQ được lập trình bằng ngôn ngữ Erlang. RabbitMQ cung cấp cho lập trình viên một phương tiện trung gian để giao tiếp giữa nhiều thành phần trong một hệ thống lớn ( Ví dụ openstack - Một công nghệ rất thú vị hi vọng một ngày nào đó tôi đủ sức để viết vài bài về chủ đề này ). RabbitMQ sẽ nhận message đến từ các thành phần khác nhau trong hệ thống, lưu trữ chúng an toàn trước khi đẩy đến đích.

RabbitMQ thiết kế để giải quyết:
- Bảo đảm message được gửi và được nhận
- Đinh tuyến message tới nới nhận chính xác
- Lưu giữ trạng thái các message
- Hỗ trợ nhiều giao thức (AMQP, MQTT, STOMP, HTTP)
- Hỗ trợ cluster, tính bảo đảm, mở rộng cao
- Nhiều plugins hỗ trợ
- Hỗ trợ đã ngôn ngữ

## Giải pháp và lợi ích
Trong một hệ thống phân tán (distributed system), có rất nhiều thành phần. Nếu muốn các thành phần này giao tiếp được với nhau thì chúng phải biết nhau. Nhưng điều này gây rắc rối cho việc viết code. Một thành phần phải biết quá nhiều đâm ra rất khó maintain, debug. Giải pháp ở đây là thay vì các liên kết trực tiếp, khiến các thành phần phải biết nhau thì sử dụng một liên kết trung gian qua một message broker. Với sự tham gia của message broker thì producer sẽ không hề biết consumer. Nó chỉ việc gửi message đến các queue trong message broker. Consumer chỉ việc đăng ký nhận message từ các queue này.


## Kiển trúc Event-driven architecture
Kiến trúc EDA bao gồm 4 thành phần: 
- Event creator hoặc producer: Nơi sản xuất event
- Event consumer: Nơi lắng nghe, xử lý
- Event manager: Lớp trung gian giữa bên tạo và bên xử lý
- Event: Hành động, sự kiện được phát hiện bơi consumer

Kiến trúc EDA giải quyết rất nhiều vấn đề trong kiến trúc phần mềm:
- Hỗ trợ lương lớn producer, consumer tham gia.
- Hỗ trợ realtime gửi, nhận message
- Ngăn chặn việc blocking, waiting phía consumer
- Hỗ trợ hoạt động bất đồng bộ

EDA

ESB

## Khái niệm về Message

### Message
Đối tượng trung tâm trong hệ thống. Có thể chứa nhiều kiểu thông tin. Ví dụ như thông tin về một process/task để khởi động một ứng dụng nào đó (nằm trên một server khác), hoặc có thể là một message chứa text đơn giản.

### Message broker
Message broker là thiết kế, kiến trúc. Message broker cho phép nhiều nơi gửi tin nhắn tới nhiều nơi nhận. Giảm sự rằng buộc giữa các thành phần trong phần mềm và tại đó, message broker như trung tâm, chuyển giao, phân phát các tin nhắn.

message-broker.png

### Message Queues
Như tên, chúng là queue các message (Đường ống các tin nhắn). Message Queue tương tự như cấu trúc dữ liệu Queue. Chúng là giải pháp cho các tiến trình đồng bộ, bất đồng bộ trong nhưng ứng dụng lớn.

message-queue.png

### Message Producers
- Như tên, chúng là nơi sản xuất ra sự kiện.
- Có thể gửi không giới hạn các sự kiện

### Message Consumers
- Consumer chịu trách nhiệm xử lý nhận, lắng nghe các sự kiện
- Consumer là điểm đến cuối cùng của message
- Xử lý các sự kiện bất đồng bộ hoặc đồng bộ

### Advanced Message Queuing Protocol (AMQP)

AMQP một giao thức internet mở và được chuẩn hóa để truyền message tin cậy giữa các ứng dụng hoặc tổ chức.

## AMQ elements
Kiến trúc AMQ (Advanced Message Queuing) gồm 4 thành phần:
- Message Flow: It explains the message life cycle
- Exchanges: It accepts messages from publisher, and then routes  to the Message Queues
- Message Queues: It stores messages in memory or disk and delivers
messages to the consumers
- Bindings: It specifies the relationship between an exchange and a message queue that tells how to route messages to the right Message Queues

(Note 69)