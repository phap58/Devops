<h2>Docker images</h2>

Docker images là các khối xây dựng của vùng chọn chứa docker. Chúng nhẹ, không thay đổi và bao gồm nhiều lớp. Docker images chứa mã ứng dụng, tệp dữ liệu, tệp cấu hình, thư viên và các phần phụ thuộc khác cần thiết để chạy ứng dụng.

<h3> Docker images và images layers</h3>
<hr>
- Giả sử Docker images như một mẫu mà từ đó các vùng chứa Docker được tạo và thực thi. Mỗi Docker images bao gồm "multiple layers" thêm hoặc xóa file trước đó. "Each layer" đại diện cho một tập hợp các thay đổi cụ thể được thực hiện đối với images và được tạo dựa trên các hướng dẫn trong Dockerfile."Dockerfile xác định cách xây dựng hình ảnh"
<br>
- Mục đích của việc "multiple layers" là giữ cho image cuối cùng nhỏ nhất có thể, thực hiện việc này bằng cách sử dụng lại các "layer" trong images và để tăng tốc quá trình xây dựng vùng chứa, vì docker chỉ phải xây dựng lại các lớp đã được thay đổi

<h3>How to build a Docker image</h3>
<br>
<Code> Chìa khóa để đóng gió ứng dụng dưới dạng docker image là phải có dockerfile. Dockerfile đóng vai trò là nguồn thông tin chính xác hoặc hướng dẫn sử dụng: Nó chỉ định cách Docker xây dựng image và chứa một loạt lệnh để xây dựng image. Mỗi lệnh xây dựng layer mới trở thành một phần của image cuối cùng. Quy trình phổ biến là bắt đầu với hình ảnh cơ sở như Debian Linux hoặc Python 3.12, cài đặt các thư viện mà ứng dụng yêu cầu, sau đó sao chép ứng dụng và mọi tệp liên quan vào hình ảnh.</code>

**example:**

<Code>FROM python:3.12</code>

        Cho thấy đăng bắt đầu từ hình ảnh cơ sở python 3.12
<code>COPY *.py setup.cfg LICENSE README.md requirements.txt /app/
<br>
WORKDIR /app
</code>

        Lệnh này yêu cầu sao chép tất cả các tệp của ứng dụng vào một thư mục bên trong vùng chứa có tên /app và đặt nó làm thư mục làm việc hiện tại.
<Code>RUN pip install -r requirements.txt
<br>
RUN python setup.py install
</code>

        Hai dòng mã này chạy các lệnh Python để cài đặt các thư viện mà ứng dụng yêu cầu. Khi bước đó hoàn tất, xây dựng và cài đặt ứng dụng bên trong vùng chứa.
<code>EXPOSE 8000
<br>
CMD [ "/usr/local/bin/my-application" ]
</code>

        Lệnh này cho Docker biết tệp thực thi nào sẽ chạy khi vùng chứa khởi động và vùng chứa đó sẽ lắng nghe các kết nối mạng trên cổng 8000.

**Để xây dựng hình ảnh này từ Dockerfile, hãy sử dụng lệnh: docker build. Nếu quá trình xây dựng thành công, Docker sẽ xuất ID của hình ảnh mới mà sau đó bạn có thể sử dụng ID này để khởi động vùng chứa.**

<h3>How to manage images</h3>
<ul>
<li><code>docker image ls</code> Lệnh này liệt kê các hình ảnh được lưu trữ cục bộ.
<li><code>docker image tag</code> Lệnh này áp dụng thẻ cho hình ảnh cục bộ.
<li><code>docker image pull</code> Lệnh này tìm nạp hình ảnh từ kho lưu trữ từ xa.
<li><code>docker image push</code> Lệnh này sẽ gửi hình ảnh cục bộ đến kho lưu trữ từ xa.
<li><code>docker image rm</code> Lệnh này xóa hình ảnh khỏi bộ đệm.
<li><code>docker image prune</code>
</ul> Lệnh này xóa tất cả các hình ảnh không sử dụng để lấy lại dung lượng ổ đĩa.