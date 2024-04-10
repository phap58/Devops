<code> gcloud init</code>
</br>
Lệnh <code>gcloud</code> init thiết lập quy trình xác thực giữa máy ảo và Google Cloud. Lưu ý rằng bạn phải đăng nhập vào tài khoản đám mây của mình để hoạt động với Google Cloud từ CLI của bạn.
</br>
<code>gcloud compute instances create --source-instance-template webserver-template ws1 ws2 ws3 ws4 ws5</code>
</br>
Dòng mã này tạo năm máy ảo mới từ mẫu máy chủ web. Trong mã này, lệnh <code>gcloud</code> gọi Google Cloud. Tham số tính toán cho biết chúng tôi đang làm việc với máy ảo. Tham số instance cho biết chúng tôi sẽ làm việc với các phiên bản VM và lệnh tạo cho biết rằng chúng tôi sẽ tạo các phiên bản mới. <code>--source -instance-template webserver-template</code> cho biết mẫu nào sẽ được sử dụng để tạo các phiên bản này. Và cuối cùng, mã<code>ws1 ws2 ws3 ws4 ws5</code> liệt kê tên của năm phiên bản sẽ được tạo khi mã này được chạy.


