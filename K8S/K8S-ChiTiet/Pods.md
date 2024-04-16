<h2>Pods</h2>

- Trong K8s, container là một gói nhẹ, độc lập, có thể thực thi được, bao gồm mọi thứ cần thiết để chạy một phần mềm, bao gồm mã, thời gian chạy, thư viện, biến môi trường và công cụ hệ thống. Container được cách ly với nhau và đóng gói phần mềm, thư viện cũng như tệp cấu hình của riêng chúng nhưng chúng chia sẻ nhân hệ điều hành với các vùng chứa khác. Chúng được thiết kế để có thể dễ dàng di chuyển trên các môi trường khác nhau, điều này khiến chúng trở nên lý tưởng để triển khai nhất quán trên các nền tảng khác nhau.

- Trong Kubernetes, container là đơn vị triển khai nhỏ nhất được lên lịch và quản lý. Chúng được gói gọn trong Pods , là đơn vị triển khai cơ bản trong cụm Kubernetes. Một Pod có thể chứa một hoặc nhiều container cần chạy cùng nhau trên cùng một máy chủ và chia sẻ cùng một mạng và tài nguyên lưu trữ, cho phép chúng giao tiếp với nhau bằng localhost.

- Pod đóng vai trò như một lớp trừu tượng, cho phép Kubernetes lên lịch và sắp xếp các container một cách hiệu quả. Khi quá trình triển khai yêu cầu nhiều vùng chứa hoạt động cùng nhau trên cùng một node, Pod sẽ được tạo để đảm bảo chúng được đặt cùng vị trí và có thể giao tiếp hiệu quả. Điều này giúp đơn giản hóa việc triển khai và quản lý các ứng dụng được đóng gói, giúp dễ dàng mở rộng quy mô, giám sát và cập nhật khi cần.

<h3>Pods as logical host</h3>

Một Pod có thể chạy một hoặc nhiều container có liên quan chặt chẽ với nhau, chia sẻ cùng bối cảnh mạng và lưu trữ. Bối cảnh được chia sẻ này rất giống với những gì bạn tìm thấy trên máy vật lý hoặc máy ảo, do đó có thuật ngữ "máy chủ logic". 

Những điểm chính cần hiểu về Pod với tư cách là máy chủ logic là:

- Các vùng chứa được liên kết chặt chẽ(Tightly coupled containers): Khi nhiều vùng chứa trong một Pod được coi là được liên kết chặt chẽ, điều đó có nghĩa là chúng có sự phụ thuộc lẫn nhau mạnh mẽ và cần liên lạc với nhau qua localhost. Điều này cho phép họ trao đổi dữ liệu và thông tin một cách hiệu quả mà không cần cấu hình mạng phức tạp.

- Không gian tên mạng dùng chung(Shared network namespace): Các vùng chứa trong cùng một Pod chia sẻ cùng một không gian tên mạng. Điều này ngụ ý rằng chúng có cùng địa chỉ IP và không gian cổng, giúp chúng giao tiếp dễ dàng hơn bằng cách sử dụng các cơ chế giao tiếp giữa các quá trình tiêu chuẩn.

- Bối cảnh lưu trữ được chia sẻ(Shared storage context): Các nhóm cũng chia sẻ cùng một bối cảnh lưu trữ, có nghĩa là chúng có thể truy cập cùng một khối lượng hoặc tài nguyên lưu trữ. Điều này tạo điều kiện thuận lợi cho việc chia sẻ dữ liệu giữa các vùng chứa trong Pod, tăng cường hơn nữa sự cộng tác của chúng.

- Đồng vị trí và đồng lập lịch(Co-location and co-scheduling): Kubernetes đảm bảo rằng tất cả các vùng chứa trong Pod đều được lên lịch và cùng đặt trên cùng một nút. Việc đồng lập kế hoạch này đảm bảo rằng các container có thể giao tiếp với nhau một cách hiệu quả trong cùng một bối cảnh mạng và lưu trữ.

- Bản chất phù du(Ephemeral nature): Giống như các vùng chứa riêng lẻ, các Pod được coi là phù du và có thể dễ dàng tạo, chấm dứt hoặc thay thế dựa trên yêu cầu mở rộng quy mô hoặc hạn chế về tài nguyên. Tuy nhiên, tất cả các thùng chứa trong Pod đều được coi là một đơn vị duy nhất về mặt lập kế hoạch và quản lý vòng đời.
