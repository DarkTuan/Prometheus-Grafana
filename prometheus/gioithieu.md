# Giới thiệu về Promethues

## Prometheus và Grafana là gì? 

Prometheus là một giải pháp giám sát open source được ban đầu được xây dựng bởi <a href='https://soundcloud.com/'>SoundCloud</a> trang âm nhạc trực tuyến.

Grafana là truy vấn dữ liệu data Prometheus để hiển thị giao diện cho đẹp và dễ nhìn.

Kiến trúc hệ thống cặp bài trùng Prometheus Monitor + Grafana

<div style="text-align:center"><img src="https://i0.wp.com/samirbehara.com/wp-content/uploads/2019/05/prometheus-architecture.png?resize=700%2C389&ssl=1"></div>

# Giải thích thành phần bên kiến trúc

- Prometheus Server: trung tâm xử lý dữ liệu
- Service discovery: Tự động tìm kiếm đối tượng đã được khai báo trong config
- AlertManager: Quản lý cảnh báo
- Grafana: Truy vấn dữ liệu từ server prome để hiển thị cho đẹp.

# Giải thích nguyên lý làm việc của Prometheus:

- Phải cài đặt node_exporter được cài đặt ở trên đối tượng cần monitor 
- Khai báo thông tin job trong config server Prometheus, để thu thập metrics, prometheus server sẽ tự pull metrics thông qua HTTP
- Sau đó thì dữ liệu được đưa xuống database của Prometheus server
- AlertManager sẽ tiến hành kiểm tra điều kiện rules của quản trị khai báo thì sẽ tự động gửi thông tin alert qua mail qua ứng dụng.
- Prometheus có Prom UI là giao diện hiển thị metric nhưng quá cùi bắp và xấu.
- Hiển thị dữ liệu đẹp hơn bằng Grafana.


Prometheus được viết bằng ngôn ngữ Go và được thiết kế theo kiến trúc microservices. 
Các thầnh phần của nó giao tiếp với nhau thông qua api 