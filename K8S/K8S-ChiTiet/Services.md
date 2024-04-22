```
Kubernetes services là gì?

Là một resouce sẽ tạo ra một single, constant point của một nhóm Pod phía sau nó. Mỗi service sẽ có một địa chỉ IP và port không đổi, trừ khi ta xóa nó đi và tạo lại. Client sẽ mở connection tới service, và connection đó sẽ được dẫn tới một trong những Pod ở phía sau.

```
<img src="https://images.viblo.asia/70712ee9-896f-4e42-a60a-baeec120abee.png">



```
Kubernetes cung cấp các loại dịch vụ khác nhau phù hợp với các yêu cầu mạng khác nhau:

ClusterIP: Tạo điều kiện giao tiếp nội bộ trong cụm

NodePort: Cho phép truy cập bên ngoài vào các dịch vụ tại một cổng tĩnh trên các nút

LoadBalancer: Cung cấp quyền truy cập bên ngoài với tính năng cân bằng tải, thường được sử dụng với bộ cân bằng tải của nhà cung cấp đám mây

Tên bên ngoài: Phục vụ như bí danh cho một dịch vụ bên ngoài, được biểu thị bằng tên DNS Kubernetes
```

```
Khám phá dịch vụ bằng DNS:

Kubernetes cung cấp dịch vụ DNS tích hợp để tự động gán tên miền cho các dịch vụ.
Giúp ứng dụng truy cập dịch vụ khác bằng tên thay vì địa chỉ IP phức tạp.
Ví dụ: database-service.default.svc.cluster.local thay vì địa chỉ IP.
Dịch vụ không đầu:

Sử dụng cho các ứng dụng đòi hỏi giao tiếp ngang hàng trực tiếp.
Không cung cấp cân bằng tải hoặc IP tĩnh như dịch vụ thông thường.
Trả về địa chỉ IP của các pod trong dịch vụ, cho phép liên lạc trực tiếp.
Cấu trúc liên kết dịch vụ:

Định tuyến lưu lượng truy cập dựa trên cấu trúc liên kết mạng (nút, vùng, v.v.).
Giảm thiểu độ trễ cho các ứng dụng phân tán trên nhiều vùng.
Ưu tiên lưu lượng truy cập đến các pod gần nhất về mặt địa lý.
Chính sách lưu lượng truy cập bên ngoài:

Bảo toàn IP nguồn máy khách cho các yêu cầu đến máy chủ web.
Định tuyến lưu lượng truy cập trực tiếp đến pod, bỏ qua cân bằng tải.
Giữ nguyên IP máy khách ban đầu cho các trường hợp sử dụng cụ thể.
Mối quan hệ phiên (phiên cố định):

Duy trì dữ liệu phiên cho người dùng trên cùng một pod.
Đảm bảo tất cả yêu cầu từ một người dùng được chuyển hướng đến cùng một pod.
Sử dụng cho các ứng dụng có trạng thái như diễn đàn web hoặc giỏ hàng.
Cắt lát dịch vụ:

Định hướng lưu lượng truy cập đến các pod khác nhau dựa trên nhãn tùy chỉnh.
Kiểm soát chi tiết việc định tuyến lưu lượng truy cập cho thử nghiệm A/B hoặc bản phát hành canary.
Thích hợp cho việc triển khai tính năng mới cho một nhóm người dùng nhỏ.
Kết nối cơ sở dữ liệu bên ngoài:

Tạo dịch vụ với loại "Tên bên ngoài" để tham chiếu cơ sở dữ liệu bên ngoài.
Cho phép ứng dụng truy cập cơ sở dữ liệu bằng tên DNS thay vì địa chỉ IP.
Tăng tính linh hoạt cho cấu hình ứng dụng và đơn giản hóa việc quản lý.
```

```
Bài học chính
Dịch vụ cung cấp một lớp trừu tượng trên Pod. 

Các dịch vụ cung cấp giải pháp kết nối mạng nhất quán và đáng tin cậy giữa các Pod tạm thời. 

Đối với các nhà phát triển Python và các nhà phát triển nói chung, Dịch vụ Kubernetes cho phép tạo ra các hệ thống phân tán mạnh mẽ và đáng tin cậy, loại bỏ sự phức tạp của mạng Pod động.

Các dịch vụ mang lại sự linh hoạt thông qua các loại cơ chế khám phá dịch vụ và cân bằng tải khác nhau, chẳng hạn như ClusterIP, NodePort, LoadBalancer và InternalName. Điều này cho phép bạn chọn cơ chế phù hợp nhất với yêu cầu của ứng dụng.
```


# Tóm tắt bài học chính về Triển khai Kubernetes:
## Lợi ích:

- Hợp lý hóa việc triển khai và quản lý ứng dụng:
    - Duy trì trạng thái mong muốn của ứng dụng.
    - Quản lý bản cập nhật và khôi phục.
    - Đảm bảo tính sẵn sàng cao.
- Tự động hóa việc triển khai và quản lý Pod và ReplicaSets:
    - Giảm thiểu gánh nặng vận hành thủ công.
    - Nâng cao hiệu quả và độ tin cậy.
- Cách tiếp cận khai báo:
    - Mô tả trạng thái mong muốn của ứng dụng.
    - Kubernetes tự động thực hiện các bước cần thiết để đạt được trạng thái đó.
    - Đảm bảo tính nhất quán và khả năng dự đoán.
- Tính sẵn sàng cao:
    - Tự động thay thế Pod bị lỗi để đảm bảo ứng dụng luôn sẵn sàng.
    - Loại bỏ điểm lỗi đơn lẻ và nâng cao khả năng phục hồi.
- Cập nhật luân phiên:
    - Triển khai bản cập nhật ứng dụng dần dần mà không gây gián đoạn dịch vụ.
    - Giảm thiểu rủi ro và đảm bảo trải nghiệm người dùng liền mạch.
- Khả năng quay lại:
    - Cho phép quay lại phiên bản ổn định trước đó trong trường hợp bản cập nhật mới gặp sự cố.
    - Giảm thiểu tác động tiêu cực và đảm bảo tính ổn định của hệ thống.
## Thành phần chính:

- Mẫu Pod mong muốn: Xác định cấu hình mong muốn cho các Pod, bao gồm hình ảnh, cổng, biến môi trường, v.v.
- Số lượng bản sao: Chỉ định số lượng Pod cần chạy để đáp ứng nhu cầu về khả năng sẵn có và khả năng mở rộng.
- Chiến lược cập nhật: Quy định cách thức triển khai bản cập nhật cho Pod, đảm bảo quá trình diễn ra suôn sẻ và không gây gián đoạn.