# Thành phần chính:

- Mẫu Pod mong muốn: Xác định cấu hình cho các Pod mà Triển khai sẽ quản lý, bao gồm:
Hình ảnh container
Cổng container
Biến môi trường
Nhãn
Các cấu hình khác
- Bản sao: Số lượng Pod giống hệt nhau của mẫu Pod sẽ chạy. Kubernetes sẽ tự động duy trì số lượng này.
- Chiến lược cập nhật: Quy định cách Triển khai xử lý cập nhật cho Pod, bao gồm:

    - Chiến lược cập nhật luân phiên (mặc định): Cập nhật dần từng Pod để đảm bảo ứng dụng luôn sẵn sàng.
    - Có thể tùy chỉnh thêm với các tham số bổ sung.
# Tính năng mạnh mẽ:

- Cập nhật khai báo:
    - Chỉ cần mô tả trạng thái mong muốn cho ứng dụng.
    - Kubernetes sẽ tự động điều chỉnh để đạt được trạng thái đó.
- Chia tỷ lệ:
    - Dễ dàng điều chỉnh số lượng Pod để xử lý tải thay đổi.
    - Ví dụ: mở rộng quy mô trong giờ cao điểm, giảm quy mô khi ít người dùng.
- Kiểm soát lịch sử và sửa đổi:
    - Theo dõi các thay đổi đối với trạng thái mong muốn.
    - Cung cấp lịch sử sửa đổi để gỡ lỗi, kiểm tra và quay lại phiên bản cụ thể.
- Lợi ích:

    - Tính sẵn sàng cao: Đảm bảo ứng dụng luôn sẵn sàng phục vụ ngay cả khi có Pod bị lỗi.
    - Khả năng mở rộng: Dễ dàng mở rộng hoặc thu hẹp ứng dụng để đáp ứng nhu cầu thay đổi.
    - Quản lý đơn giản: Cung cấp cách thức khai báo để quản lý trạng thái mong muốn của ứng dụng.
Theo dõi và kiểm soát: Cho phép theo dõi lịch sử thay đổi và quay lại phiên bản cụ thể.

## Triển khai Kubernetes thường được xác định bằng tệp YAML chỉ định các thành phần này. Đây là một ví dụ về bảng kê khai YAML.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  selector:
	matchLabels:
  	app: example-app
  template:
	metadata:
  	labels:
    	app: example-app
	spec:
  	containers:
  	- name: example-container
    	image: example-image:latest
    	ports:
    	- containerPort: 80
```
- Nội dung:

    - Triển khai này sẽ tạo và duy trì 3 bản sao của Pod chạy ứng dụng Python.
    - Mỗi Pod sẽ chạy hình ảnh example-image:latest và phơi bày cổng 80.
    - Chiến lược cập nhật luân phiên sẽ được sử dụng để cập nhật ứng dụng mà không gây gián đoạn dịch vụ.
- Lợi ích:

    - Tính sẵn sàng cao: Đảm bảo ứng dụng luôn sẵn sàng phục vụ ngay cả khi có Pod bị lỗi.
    - Khả năng mở rộng: Dễ dàng mở rộng hoặc thu hẹp ứng dụng để đáp ứng nhu cầu thay đổi.
    - Cập nhật mượt mà: Triển khai tự động cập nhật ứng dụng mà không gây gián đoạn dịch vụ.
    - Quản lý hiệu quả: Triển khai cung cấp cách thức đơn giản để quản lý vòng đời của ứng dụng Python.