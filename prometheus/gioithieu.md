# Tổng quan về prometheus 

## 1. Prometheus là gì? 

Prometheus là một giải pháp giám sát mã nguồn mở được ban đầu được xây dựng bởi <a href='https://soundcloud.com/'>SoundCloud</a>. Hệ thống giám sát Monitor

## 2. Tính năng? 

Prom có những tính năng chính như sau: 

- Mô hình dữ liệu đa chiều với dữ liệu time series(TSDB) được xác định metric name và cặp key-value 
- Sử dụng ngôn ngữ truy vấn PromQL 
- Không phụ thuộc vào distributed storage
- Thu thập metric thông qua HTTP 
- Đẩy metric đã được hỗ trợ bởi một gateway trung gian 
- Targets được tự động discovery thông qua service discovery trong prom 
- Được hỗ trợ bởi nhiều graphing và dashboarding 

## 3. Các thành phần trong promtheus 

Hệ sinh thái của giải pháp bao gồm nhiều thành phần trong đó có một vài thành phần là tùy chọn ( tức là có thể có hoặc không )

- **Prometheus server** thu thập thông tin dữ liệu 
- **Client libraries** hỗ trợ các ngôn ngữ lập trình khác tương tác với prom 
- Các **node_exporter** khai báo giám sát service: nginx, apache, openVPN server, các device 
- Một **alertmanager** phụ vụ cho việc cảnh báo 
- Cùng với các tool hỗ trợ khác nữa ...

## 4. Kiến trúc của Prometheus 

Sơ đồ này minh họa kiến ​​trúc của Prometheus và một số thành phần trong hệ sinh thái của nó:

<div style="text-align:center"><img src="https://i0.wp.com/samirbehara.com/wp-content/uploads/2019/05/prometheus-architecture.png?resize=700%2C389&ssl=1"></div>

Các làm việc của promtheus được mô tả như sau: 

- Metrics sẽ thu tập thông qua exporter 
- Prometheus sẽ tự discovery ra target của các jobs hoặc trong file cấu hình thủ công để pull metrics về 
- Sau đó prom server sẽ xử lý và lưu trữ xuống database của mình
- Cùng lúc đó AlertManager sẽ tiến hành kiểm tra điều kiện nếu match với các rules đã được người quản trị định nghĩa thì sẽ gửi cảnh báo thông qua các kênh mail, slack, ... 
- Prom UI là nơi hiển thị graph của các metrics đẩy về hệ thống. Ngoài ra garafa cũng hỗ trợ data source prom. 

Prom được viết bằng ngôn ngữ Go và được thiết kế theo kiến trúc microservices. Các thầnh phần của nó giao tiếp với nhau thông qua api 