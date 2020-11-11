# Các khái niệm được đề cập trong Promtheus 

## 1. Data model (Mô Hình Dữ Liệu)

Prometheus về cơ bản lưu trữ tất cả dữ liệu dưới dạng time series

### Metric names and labels

Mỗi time series được xác định duy nhất bởi tên metric name hoặc là labels(nhãn).

- Metric name chỉ định các thông số của của hệ thống (Vd: `http_requests_total` - tổng số request HTTP đã nhận). Nó có thể chứa các chữ cái và chữ số ASCII cũng như dấu gạch dưới và dấu hai chấm.
- labels(nhãn): Dễ hiểu là những thông tin cụ thể trong request HTTP mà metric name gửi yêu cầu request.

Ví dụ:
        `api_http_requests_total{method="POST", handler="/messages"}`

- Một time series có metric name là `api_http_requests_total` và labels `method="POST"`, `handler="/messages` cho dễ hiểu

## 2. Metric types 

Đại khái đơn giản và dễ hiểu nhất là dữ liệu theo dạng metric thì nó sẽ gửi liên tục và sẽ có 4 loại metric sau:

- Loại **counter**: là một bộ đếm tích lũy, được đặt về 0 khi restart. Ví dụ, có thể dùng counter để đếm số request được phục vụ, số lỗi, số task hoàn thành,...
. Không sử dụng cho gía trị có thể giảm như số tiến trình đang chạy.

- Loại **gauge**: đại diện cho số liệu duy nhất, nó có thể lên hoặc xuống. Nó thường được sử dụng cho các giá trị đo

- Loại **histogram**: lấy mẫu quan sát (thường là những thứ như là thời lượng yêu cầu, kích thước phản hồi). Nó cũng cung cấp tổng của các giá trị đó.

- Loại **summary**: tương tự histogram, nó cung cấp tổng số các quan sát và tổng các giá trị đó, nó tính toán số lượng có thể cấu hình qua sliding time window.

## 3. Jobs và Instances

Scrape: hiểu đơn giản là lấy thông tin

Prometheus quy định một endpoint mà bạn có thế thể scrape được gọi là một instance. 

Tập hợp của các instances có cùng một mục đích được gọi là một job 

Ví dụ: 

- job: `api-server`
    + instance 1: `IP_HOST:PORT`
    + instance 2: `IP_HOST:PORT`
    + instance 3: `IP_HOST:PORT`
    + instance 4: `IP_HOST:PORT`