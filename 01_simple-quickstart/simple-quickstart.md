# Bắt đầu nhanh Apache Kafka

Trong hướng dẫn này chúng ta sẽ tạo cài đặt và bắt đầu nhanh với Apache Kafka để  biết cách mà Kafka làm việc như thế nào.

## Bước 1: Download Kafka 

Tải về  bản release 2.3.0 và giải nén.

```
> tar -xzf kafka_2.12-2.3.0.tgz
> cd kafka_2.12-2.3.0
```

## Bước 2: Khởi động máy chủ

Kafka sử dụng ZooKeeper, vì vậy trước tiên bạn cần khởi động máy chủ ZooKeeper. Nếu bạn chưa có bạn có thể sử dụng tập lệnh được đóng gói với kafka để  lấy ví dụ tạo nhanh một node ZooKeeper.

```
> bin/zookeeper-server-start.sh config/zookeeper.properties
[2013-04-22 15:01:37,495] INFO Reading configuration from: config/zookeeper.properties (org.apache.zookeeper.server.quorum.QuorumPeerConfig)
...
```

Bây giờ khởi động máy chủ Kafka:

```
> bin/kafka-server-start.sh config/server.properties
[2013-04-22 15:01:47,028] INFO Verifying properties (kafka.utils.VerifiableProperties)
[2013-04-22 15:01:47,051] INFO Property socket.send.buffer.bytes is overridden to 1048576 (kafka.utils.VerifiableProperties)
...
```

## Bước 3: Tạo một chủ đề  (Topic)

Một topic cho phép đẩy dữ liệu vào, các Consumer khi subcribe topic này sẽ nhân được dữ liệu từ topic đẩy về.

Tạo một Topic có tên là "mytest" với một phân vùng duy nhất và chỉ một bản sao:

```
> bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic mytest
```

Bây giờ chúng ta có thể thấy chủ đề đó nếu chúng ta chạy lệnh danh sách chủ đề:

```
> bin/kafka-topics.sh --list --bootstrap-server localhost:9092
test
```

Ngoài ra, thay vì tạo chủ đề theo cách thủ công, bạn cũng có thể định cấu hình cho người môi giới của mình để tự động tạo chủ đề khi chủ đề không tồn tại được xuất bản.

## Bước 4: Gửi một số tin nhắn (Message)

Kafka đi kèm với một máy khách dòng lệnh sẽ lấy đầu vào từ một tệp hoặc từ đầu vào tiêu chuẩn và gửi nó dưới dạng tin nhắn đến cụm Kafka. Theo mặc định, mỗi dòng sẽ được gửi dưới dạng một tin nhắn riêng.

Chạy Producer (nhà sản xuất) và sau đó nhập một vài tin nhắn cửa sổ  terminal để gửi đến máy chủ Kafka.

```
> bin/kafka-console-producer.sh --broker-list localhost:9092 --topic mytest
This is a message
This is another message
```

## Bước 5: Tạo một Consumer

Kafka cũng cho phép chạy một Consumer dưới dạng dòng lệnh như sau:

```
> bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic mytest --from-beginning
This is a message
This is another message
```

Nếu bạn có mỗi lệnh trên đang chạy trong một thiết bị đầu cuối khác nhau thì bây giờ bạn có thể nhập tin nhắn vào thiết bị đầu cuối của Producer và thấy chúng xuất hiện trong thiết bị đầu cuối của Consumer (người tiêu dùng).

Chờ một chút và quan sát trong cửa sổ Termial của Consumer bạn sẽ nhận được tin nhắn từ Topic gửi về  (Topic mà đã subscribe ở trên)

## Tham khảo

Trên đây là một ví dụ để khởi động nhanh mỗi khi cần test Kafka mà mình hay dùng. Các bạn có thể xem chi tiết tại trang chủ Apache Kafka tại đây: [https://kafka.apache.org/quickstart](https://kafka.apache.org/quickstart)