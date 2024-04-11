<h1>Ansible</h1>
<hr/>
<p>Ansible là một hệ thống tự động hóa CNTT cực kỳ đơn giản. Nó xử lý việc quản lý cấu hình, triển khai ứng dụng, cung cấp đám mây, thực thi tác vụ đặc biệt, tự động hóa mạng và điều phối nhiều nút. Ansible thực hiện dễ dàng các thay đổi phức tạp như cập nhật luân phiên không có thời gian ngừng hoạt động với bộ cân bằng tải. Thông tin thêm trên trang web Ansible .</p>
<h1>Nguyên tắc thiết kế</h1>
<hr/>
<p>
<ul>
<li>Có quy trình thiết lập cực kỳ đơn giản với thời gian học tập tối thiểu.</li>
<li>Quản lý máy nhanh chóng và song song.</li>
<li>Tránh các tác nhân tùy chỉnh và các cổng mở bổ sung, không cần tác nhân bằng cách tận dụng daemon SSH hiện có.</li>
<li>Mô tả cơ sở hạ tầng bằng ngôn ngữ thân thiện với cả máy móc và con người.</li>
<li>Tập trung vào tính bảo mật và khả năng kiểm tra/đánh giá/viết lại nội dung dễ dàng.</li>
<li>Quản lý các máy từ xa mới ngay lập tức mà không cần khởi động bất kỳ phần mềm nào.</li>
<li>Cho phép phát triển mô-đun bằng bất kỳ ngôn ngữ động nào, không chỉ Python.
Có thể sử dụng được khi không phải root.</li>
<li>Hãy trở thành hệ thống tự động hóa CNTT dễ sử dụng nhất từ ​​trước đến nay.</li>
</ul>
</p>
<hr />
<h1>Sử dụng Ansible</h1>
<p>
Bạn có thể cài đặt phiên bản Ansible đã phát hành bằng <code>pip</code> hoặc trình quản lý gói. Xem hướng dẫn cài đặt Ansible trên nhiều nền tảng khác nhau.
<h3>Cài đặt và nâng cấp với <code>pipx</code></h3>
<h4>Installing Ansible</h4>
<ul>
<li>
Sử dụng pipxtrong môi trường của bạn để cài đặt gói Ansible đầy đủ:
<p>
<code>
pipx install --include-deps ansible
</code>
</p>
</li>
<li>
Bạn có thể cài đặt ansible-coregói tối thiểu:
<p>
<code>
pipx install ansible-core
</code>
</p>
</li>
<li>
Ngoài ra, bạn có thể cài đặt một phiên bản cụ thể của ansible-core:
<p>
<code>
pipx install ansible-core==2.12.3
</code>
</p>
</li>
</ul>
<h4>Upgrading Ansible</h4>
<ul>
<li>
Để nâng cấp bản cài đặt Ansible hiện có lên phiên bản phát hành mới nhất:
<p>
<code>
pipx upgrade --include-injected ansible
</code>
</p>
</li>
</ul>
<h4>Installing Extra Python Dependencies</h4>
<ul>
<li>
Để cài đặt các phụ thuộc python bổ sung có thể cần thiết, với ví dụ về cài đặt argcompletegói python như được mô tả bên dưới:
<p><code>
pipx inject ansible argcomplete
</code></p>
</li>
<li>
Bao gồm --include-appstùy chọn tạo ứng dụng trong phần phụ thuộc python bổ sung có sẵn trên PATH của bạn. Điều này cho phép bạn thực thi các lệnh cho các ứng dụng đó từ shell.
<p><code>
pipx inject --include-apps ansible argcomplete
</code></p>
</li>
</ul>
<h3>Cài đặt và nâng cấp bằng<code> pip</code></h3>
<h4>Ensuring <code>pip</code> is available</h4>
<ul>
<li>
Để xác minh xem pipPython ưa thích của bạn đã được cài đặt chưa:
<p><code>
python3 -m pip -V
</code></p></li>
<li>
Nếu tất cả đều ổn, bạn sẽ thấy một cái gì đó như sau:
<p><code>
python3 -m pip -V
pip 21.0.1 from /usr/lib/python3.9/site-packages/pip (python 3.9)
</code></p></li>
<li>
Nếu <code>pip</code> có, bạn có thể chuyển sang bước tiếp theo .
</li>
<li>
Nếu gặp lỗi như <code>No module named pip</code> , bạn sẽ cần cài đặt <code> pip</code> bằng trình thông dịch Python đã chọn trước khi tiếp tục. Điều này có thể có nghĩa là cài đặt gói hệ điều hành bổ sung (ví dụ: <code>python3-pip</code>) hoặc cài đặt gói mới nhất trực tiếp từ <code>pip</code> Cơ quan đóng gói Python bằng cách chạy như sau:
<p><code>
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py --user</code></p></li>
</ul>
<h4>Installing Ansible</h4>
<ul>
<li>
Sử dụng <Code>pip</code> trong môi trường Python đã chọn của bạn để cài đặt gói Ansible đầy đủ cho người dùng hiện tại:
<p><code>
python3 -m pip install --user ansible
</code></p></li>
<li>
Bạn có thể cài đặt <code>ansible-core</code> gói tối thiểu cho người dùng hiện tại:
<p><code>
python3 -m pip install --user ansible-core
</p></code></li>
<li>
Ngoài ra, bạn có thể cài đặt một phiên bản cụ thể của <code> ansible-core</code>:
<p><code>
python3 -m pip install --user ansible-core==2.12.3</p></code></li>
</ul>
<h4>Upgrding Ansible</h4>
<ul>
<li>
Để nâng cấp bản cài đặt Ansible hiện có trong môi trường Python này lên phiên bản phát hành mới nhất, chỉ cần thêm <code>--upgrade</code> vào lệnh trên:
<p><code>
python3 -m pip install --upgrade --user ansible</code></p></li>
</ul>
Người dùng và nhà phát triển thành thạo có thể develtrực tiếp điều hành nhánh có các tính năng và bản sửa lỗi mới nhất. Mặc dù nó khá ổn định nhưng bạn có nhiều khả năng gặp phải những thay đổi đột phá khi chạy nhánh devel. Chúng tôi khuyên bạn nên tham gia vào cộng đồng Ansible nếu bạn muốn điều hành chi develnhánh.
</p>