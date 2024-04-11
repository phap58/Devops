<h2>KHÁI NIỆM</H2  >
<h3>Module</h3>
<p>
Module hay các thư viện module cung cấp cho Ansible các thư viện để điều khiển hoặc quản lý tài nguyên trên local hoặc các remote các server.
</p>
<hr>
<h3>Playbook</h3>
<p>
<ul>
<li> Ansible playbook được viết bằng cú pháp YAML. Nó có thể chứa nhiều hơn một play. Mỗi play chứa tên các nhóm máy chủ để kết nối tới và các nhiệm vụ ,à nó cần thực hiện. Nó cũng có chứa các biến/các role/các handler, nếu đã định nghĩa.
<li> Một ví dụ về playbook :

        ---

        - hosts: dbservers
        gather_facts: no

        vars:
        who: World

        tasks:
        - name: say hello
        debug: msg="Hello {{ who }}"

        - name: retrieve the uptime
        command: uptime
</ul>
</p>
<hr>
<h3>Inventory</h3>
<p>
<ul>
<li>File iventory để giúp Ansible biết các server mà nó cần kết nối sử dụng SSH , thông tin kết nối nó yêu cầu và các tùy chọn biến gắn liền với các server này.
<li>File inventory có định dạng là INI. Trong file inventory, chúng ta có thể chỉ định nhiều hơn một máy chủ và gom chúng thành nhiều nhóm.
<li>Ví dụ file iventory hosts.ini như sau :

        [dbservers]
db.example.com

</ul>
</p>
<hr>
<h3>Task</h3>
<p>
<ul>
<li>Một khái niệm quan trọng khác đó là nhiệm vụ. Mỗi nhiệm của Ansible chưa một tên, một module để gọi , các tham số của module, và tùy chọn các điều kiện trước sau. Chúng cho phép chúng ta gọi các module Ansible và truyền thông tin tới các nhiệm vụ liên tiếp.

</ul>
</p>
<hr>
<h3>Các biến (vars)</h3>
<p>
<ul>
<li>Biến rất hữu dụng trong việc tái sử dụng thông tin chúng ta cung cấp hoặc tập hợp . Chúng ta có thể định nghĩa biến trong các file iventory, các file YAML hoặc trong các playbook.

</ul>
</p>