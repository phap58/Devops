<code> gcloud init</code>
</br>
Lệnh <code>gcloud</code> init thiết lập quy trình xác thực giữa máy ảo và Google Cloud. Lưu ý rằng bạn phải đăng nhập vào tài khoản đám mây của mình để hoạt động với Google Cloud từ CLI của bạn.
</br>
<code>gcloud compute instances create --source-instance-template webserver-template ws1 ws2 ws3 ws4 ws5</code>
</br>
Dòng mã này tạo năm máy ảo mới từ mẫu máy chủ web. Trong mã này, lệnh <code>gcloud</code> gọi Google Cloud. Tham số tính toán cho biết chúng tôi đang làm việc với máy ảo. Tham số instance cho biết chúng tôi sẽ làm việc với các phiên bản VM và lệnh tạo cho biết rằng chúng tôi sẽ tạo các phiên bản mới. <code>--source -instance-template webserver-template</code> cho biết mẫu nào sẽ được sử dụng để tạo các phiên bản này. Và cuối cùng, mã <code>ws1 ws2 ws3 ws4 ws5</code> liệt kê tên của năm phiên bản sẽ được tạo khi mã này được chạy.


*KHÁI NIỆM:

Script in ra một dòng duy nhất cho biết nó đang lắng nghe các kết nối trên cổng 8000. Điều đang xảy ra phía sau hậu trường là ứng dụng đang mở một socket và lắng nghe các kết nối HTTP trên cổng đó. Trong trường hợp này, nó đang chạy trên cổng 8000.

Chúng ta có những lựa chọn nào? Script thực sự cho phép chúng tôi truyền số cổng mà nó sẽ mở dưới dạng tham số. muốn nó chạy trên cổng HTTP mà chúng tôi đã cấu hình trong video trước đó là cổng 80. Và vì đây là cổng hệ thống, để ứng dụng sử dụng nó, cần chạy nó với quyền quản trị. Vì vậy, hãy dừng tiến trình đang chạy ngay bây giờ bằng cách nhấn Ctrl + C. Và sau đó chạy lại nó với sudo và truyền cổng 80 làm tham số.

Dừng sudo 80.

Đây là tệp systemd, hệ thống khởi tạo được sử dụng bởi hầu hết các bản phân phối Linux hiện đại. Đừng lo lắng nếu bạn không hiểu chuyện gì đang xảy ra ở đây.

không cần phải hiểu các chi tiết của tệp này để biết cách triển khai dịch vụ lên đám mây. Chỉ cần lưu ý rằng cấu hình mong đợi script mà muốn thực thi nằm trong / usr / local / bin.

cần sao chép tệp đó vào đó và sau đó sao chép tệp dịch vụ vào / etc / systemd / system, đây là thư mục được sử dụng để cấu hình các dịch vụ systemd. Và cuối cùng, cần thông báo cho lệnh systemctl rằng chúng tôi muốn bật dịch vụ này để nó chạy tự động.

bất cứ khi nào máy này khởi động, nó sẽ khởi động ứng dụng web mà chúng tôi đã cấu hình và chúng tôi sẽ có thể thấy nội dung mà chúng tôi đã thấy trước đó. Hãy thử bằng cách kích hoạt khởi động lại.


