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

<h3>Ưu điểm của Pod</h3>

- Tạo điều kiện cho việc đặt cùng vị trí(Facilitating co-location): Các nhóm cho phép nhiều vùng chứa được đặt cùng vị trí trên cùng một máy chủ. Điều này đặc biệt hữu ích cho các thành phần có liên quan chặt chẽ cần hoạt động cùng nhau, chẳng hạn như một ứng dụng và các thành phần trợ giúp của nó (như các thùng chứa sidecar xử lý việc ghi nhật ký hoặc giám sát). Bằng cách chạy các thành phần này trong cùng một Pod, chúng có thể được lên lịch trên cùng một máy và được quản lý dưới dạng một thực thể duy nhất.

- Cho phép chia sẻ dữ liệu(Enabling data sharing): Các vùng chứa trong Pod chia sẻ cùng một không gian tên mạng, nghĩa là chúng chia sẻ địa chỉ IP và không gian cổng. Họ có thể liên lạc với nhau bằng localhost và họ cũng có thể chia sẻ dữ liệu thông qua các khối được chia sẻ. Các khối được chia sẻ trong Pod cho phép dữ liệu được trao đổi dễ dàng giữa các vùng chứa và cũng cho phép dữ liệu tồn tại lâu hơn tuổi thọ của một vùng chứa duy nhất, điều này có thể hữu ích cho các ứng dụng yêu cầu lưu trữ dữ liệu liên tục.

- Đơn giản hóa giao tiếp giữa các container(Simplifying inter-container communication): Không gian tên mạng dùng chung cũng đơn giản hóa giao tiếp giữa các container. Bởi vì tất cả các bộ chứa trong Pod đều chia sẻ một ngăn xếp mạng nên chúng có thể giao tiếp với nhau trên localhost mà không cần giao tiếp giữa các quá trình (IPC) hoặc hệ thống tệp dùng chung. Điều này giúp đơn giản hóa việc phát triển các hệ thống phân tán, nơi các thành phần thường cần giao tiếp với nhau.

<h3>So sánh 1 container với nhiều container </h3>

Sự khác biệt giữa Pod một container và Pod nhiều container nằm ở số lượng container mà chúng lưu trữ.

Đúng như tên gọi, Pod một container chỉ chứa một container. Vùng chứa này thường đại diện cho ứng dụng hoặc dịch vụ chính mà Pod định chạy. Pod một container rất đơn giản và thường được sử dụng khi bạn có một ứng dụng đơn giản không yêu cầu thêm thùng chứa sidecar hoặc các thành phần trợ giúp có liên quan chặt chẽ. Chúng cũng thích hợp để chạy các ứng dụng độc lập không cần giao tiếp với các vùng chứa khác trong cùng một Pod. 

Mặt khác, các Pod nhiều vùng chứa chứa nhiều vùng chứa được đặt cùng vị trí và chia sẻ cùng một tài nguyên cũng như không gian tên mạng. Những thùng chứa này nhằm mục đích làm việc cùng nhau và bổ sung các chức năng của nhau. Pod nhiều container thích hợp trong nhiều trường hợp khác nhau:  	

Mẫu sidecar: Mẫu sidecar là trường hợp sử dụng phổ biến cho Pod nhiều container. Trong mẫu này, vùng chứa chính đại diện cho ứng dụng chính, trong khi vùng chứa sidecar bổ sung cung cấp các tính năng hỗ trợ như ghi nhật ký, giám sát hoặc xác thực. Các thùng chứa sidecar nâng cao và mở rộng khả năng của ứng dụng chính mà không cần sửa đổi mã của nó.

Mẫu proxy: Pod nhiều vùng chứa có thể sử dụng vùng chứa proxy hoạt động như một trung gian giữa vùng chứa ứng dụng chính và thế giới bên ngoài. Vùng chứa proxy xử lý các tác vụ như cân bằng tải, lưu vào bộ đệm hoặc chấm dứt SSL, giảm tải các trách nhiệm này khỏi vùng chứa ứng dụng chính.

Mẫu bộ điều hợp: Pod nhiều vùng chứa có thể sử dụng bộ chứa bộ điều hợp để thực hiện chuyển đổi định dạng dữ liệu hoặc dịch giao thức. Điều này cho phép vùng chứa chính chỉ tập trung vào chức năng cốt lõi của nó mà không phải lo lắng về sự phức tạp của các định dạng trao đổi dữ liệu.

Dữ liệu được chia sẻ và các phần phụ thuộc: Các vùng chứa trong Pod nhiều vùng chứa có thể chia sẻ khối lượng và giao tiếp qua localhost, khiến chúng phù hợp với các ứng dụng yêu cầu chia sẻ dữ liệu hoặc có các thành phần phụ thuộc lẫn nhau.

Sử dụng Pod một vùng chứa khi bạn có một ứng dụng đơn giản không yêu cầu vùng chứa bổ sung hoặc khi bạn muốn tách biệt các ứng dụng hoặc dịch vụ khác nhau để quản lý và mở rộng quy mô dễ dàng hơn. 

Sử dụng Pod nhiều vùng chứa khi bạn có các thành phần liên quan chặt chẽ cần hoạt động cùng nhau, chẳng hạn như những thành phần theo mẫu sidecar. Điều này hữu ích cho các tác vụ như ghi nhật ký, giám sát hoặc nâng cao khả năng của ứng dụng chính mà không cần sửa đổi mã của ứng dụng đó. Pod nhiều vùng chứa cũng thích hợp cho các tình huống trong đó nhiều vùng chứa cần chia sẻ dữ liệu hoặc phần phụ thuộc một cách hiệu quả.

```

Bài học chính
Pod là đơn vị triển khai cơ bản trong cụm Kubernetes. 

Một Pod có thể chứa một hoặc nhiều container cần chạy cùng nhau trên cùng một máy chủ và chia sẻ cùng một mạng và tài nguyên lưu trữ, cho phép chúng giao tiếp với nhau bằng localhost.

Pod đóng vai trò như một lớp trừu tượng, cho phép Kubernetes lên lịch và sắp xếp các container một cách hiệu quả.

Sử dụng Pod một vùng chứa khi bạn có một ứng dụng đơn giản không yêu cầu vùng chứa bổ sung hoặc khi bạn muốn tách biệt các ứng dụng hoặc dịch vụ khác nhau để quản lý và mở rộng quy mô dễ dàng hơn. 

Sử dụng Pod nhiều vùng chứa khi bạn có các thành phần liên quan chặt chẽ cần hoạt động cùng nhau, chẳng hạn như những thành phần theo mẫu sidecar. 
```