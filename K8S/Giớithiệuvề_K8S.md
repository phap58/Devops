<h2>GIỚI THIỆU VỀ K8S</h2>
<p>
<code>Kubernetes chỉ là một phần trong hệ sinh thái của container ngày nay</code> do vậy trước khi đi vào tìm hiểu về Kubernetes, chúng ta cần biết tổng quan về hệ sinh thái của container. Trong hệ sinh thái của container có 03 phần chính, bao gồm: 
<ul>
<li>Phần 1: Đây là thành phần cơ bản và cốt lõi nhất trong hệ sinh thái container, các thành phần này bao gồm: Kiến trúc lõi của container (các khái niệm về runtime spec, image format speck); khái niệm images, network và storage.
<li>Phần 2: Các công nghệ về platform liên quan tới container, bao gồm: các sản phẩm để orchestration container (sử dụng để khởi tạo các container theo các cơ chế điều phối), nền tảng để quản lý các container và các nền tảng PaaS dựa trên container.
<li>Phần 3: Các công nghệ hỗ trợ container, bao gồm: công nghệ hỗ trợ khi triển khai container trên nhiều máy chủ vật lý, các giải pháp phụ trợ về thu thập log và gaims sát.
<img src="../K8S/img/Docker-ecosys1.png">
<li>Kubernetes là một sản phẩm nằm trong phần 2 của hệ sinh thái của container hiện nay. Nó đóng vai trò là là một công cụ orchestration (tạo ra, điều phối và chỉ huy các container) - nôm na mà nói thì kubernetes là thằng túm đầu các máy vật lý hoặc máy ảo được cài đặt môi trường để triển khai container.
</ul>
</p>
<hr>
<h2>Các thông tin khởi đầu với K8s</h2>
<h3>Trước khi bắt đầu tìm hiểu về K8S, cần có: </h3>
<ul>
<li> Vừa đọc khái niệm lý thuyết + thực hành
<li> Tìm hiểu về container + docker ở mức bas
<li> Kỹ năng và kiến thức làm việc với K8S: Linux
<li> Network, web server, db
</ul>
<h3>Cách cài đặt K8S</h3>
<p>K8S có rất nhiều cách cài (công cụ khác nhau) khác nhau, tùy ngữ cảnh mà áp dụng. Tựu chung lại có 02 phương pháp cài đặt chính, đó là cài bằng tay và cài tự động (tự động thông qua các tools hoặc script mà bên khác cung cấp).
</p>
<ul>
<li>Cài bằng tay: Có nghĩa là cài theo kiểu step by step theo tài liệu của K8S.
<ul>
<li>
Cài bằng tay thì tốn nhiều thời gian (có cách khắc phục là viết script hoặc lợi dụng các tools ở dưới) nhưng mang lại lợi ích về việc nắm chắc các bước nếu như bỏ thời gian đọc và cài theo.
<li>
Thích hợp với các môi trường phục vụ chạy production hoặc mô trường có nhiều host vật lý.
<li>
Cài bằng tay bằng các lệnh hoặc biên dịch từ mã nguồn mà K8S cung câp.
</ul>
<li><Code>Minikube</code>: Là một công cụ để cài đặt K8S - sử dụng nó như là cách bạn sử dụng mỳ ăn liền ấy. <code>Minikube</code> có các đặc điểm sau:
<ul>
<li><code>Minikube</code> có thể hiểu là mì ăn liền trong thực tế, như vậy nó có tương đối các thành phần để đảm bảo K8S hoạt động được.
<li><code>Minikube</code> thích hợp với việc thử nghiệm ban đầu và thường cài trên 1 máy.</code>
<li><code>Minikube</code> có thể chạy trên nhiều hệ điều hành khác nhau nhưng tốt nhất nên có một máy Ubuntu hoặc Centos để cài Minikube
</ul>
<li>Cài bằng các tools đã được chế lại theo môi trường triển khai, tùy vào nhà cung cấp dịch vụ mà họ sẽ cung cấp các công cụ cài hoặc thậm chí đã cài sẵn (tự tìm hiểu trên gg)
</ul>