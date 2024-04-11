#MỘT SỐ CHÚ Ý VỀ ANSIBLE
<p>
<h3>#1. Về cú pháp YAML
</h3>
<ul>
<li>
YAML bắt đầu bằng --- và kết thúc bằng ...
</li>
<li>
YAML sử dụng indent là 2 space. Chú ý về space, chỉ cần thừa hoặc thiếu 1 space là có thể sai ngay.
</li>
<li>
Text editor có thể là:
<ul>
<li>
Notepad ++.
<li>
Sublime Text.
<li>
Atom.
<li>
....
</ul>
<li>
Đối với Notepad++, bạn cần chuyển đổi <code>TABs to spaces</code> để có thể dễ dàng chỉnh sửa file yaml với phím TAB. Nếu không, thì không nên sử dụng phím TAB để trong yaml.
<li>
Để thực hiện, vào <code>Settings -> Preferences -> Tab Settings</code>, rồi chọn như hình dưới đây. 
<li>
Để check cú pháp YAML, mình có 2 cách sau đây:

Rất đơn giản, truy cập trang web http://www.yamllint.com/, post đoạn yaml cần check và nhấn GO. Trang web sẽ trả về kết quả cho bạn.
Sử dụng Plugin Pretty YAML với Sublime Text. Chi tiết tại đây: https://packagecontrol.io/packages/Pretty%20YAML
<hr>
<h3>#2. Về Ansible</h3>
<ul>
<li>Ansible hỗ trợ rất nhiều module để mình có thể viết playbooks. Chỉ cần search từ khóa + ansible là có thể tìm ra.
<li>Ansible Galaxy, một kho tàng các roles mà mọi người trên toàn thế giới có thể đóng góp. Muốn triển khai một cái gì đó, hãy thử search trên Ansible Galaxy xem đã có chưa. “Ansible Galaxy” can either refer to a website for sharing and downloading Ansible roles, or a command line tool for managing and creating roles Chi tiết tại https://galaxy.ansible.com/
<li>Cấu trúc một playbook chuẩn</li>



        production                # inventory file for production servers
        staging                   # inventory file for staging environment

        group_vars/
        group1                 # here we assign variables to particular groups
        group2                 # ""
        host_vars/
        hostname1              # if systems need specific variables, put them here
        hostname2              # ""

        library/                  # if any custom modules, put them here (optional)
        filter_plugins/           # if any custom filter plugins, put them here (optional)

        site.yml                  # master playbook
        webservers.yml            # playbook for webserver tier
        dbservers.yml             # playbook for dbserver tier

        roles/
            common/               # this hierarchy represents a "role"
                tasks/            #
                    main.yml      #  <-- tasks file can include smaller files if warranted
                handlers/         #
                    main.yml      #  <-- handlers file
                templates/        #  <-- files for use with the template resource
                    ntp.conf.j2   #  <------- templates end in .j2
                files/            #
                    bar.txt       #  <-- files for use with the copy resource
                    foo.sh        #  <-- script files for use with the script resource
                vars/             #
                    main.yml      #  <-- variables associated with this role
                defaults/         #
                    main.yml      #  <-- default lower priority variables for this role
                meta/             #
                    main.yml      #  <-- role dependencies

            webtier/              # same kind of structure as "common" was above, done for the webtier role
            monitoring/           # ""
            fooapp/               # ""


</ul>