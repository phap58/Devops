<h2>Ghi chép về Playbook trong Ansible</h2>

<ul>
<li> Task là một việc hay yêu cầu được thực hiện trong Ansible
<li> Mỗi <code>task</code> trong ansible là một play
-> thực hiện từng task một theo thứ tự mà chúng được định nghĩa trong playbook, và báo cáo kết quả sau khi hoàn thành -> tự động hóa việc quản lý hệ thống và triển khai một cách hiệu quả
<li> Nhiều play kết hợp lại gọi là <code> Playbook</code>
</ul>

<Hr>
<h4>Cú pháp</h4>
<ul>
<li> Câu lệnh:

        ansible-playbook file_yaml.yml
</ul>
<h4>Ghi chú</h4>
<ul>
<li> Sử dụng Playbook với file host cụ thể, sử dụng tùy chọn <code>-i</code>
<li> Minh họa

<p>Sử dụng dụng tùy chọn <Code>--list-hosts</code> trong <Code>playbook</code> để kiểm tra các host được áp dụng.</p>
<li> Minh họa

<p>Sử dụng dụng tùy chọn <Code>--list-task</code> trong <Code>playbook</code> để kiểm tra các task trong playbook.</p>
<li> Minh họa

<p>Sử dụng tùy chọn <code>--step</code> để thực hiện từng task sau khi người dùng nhập vào
</p>

         ansible-playbook -i /root/ansible-vd1/hosts  /root/ansible-vd1/installhttp.yml --step
<li> Minh họa

</ul>

