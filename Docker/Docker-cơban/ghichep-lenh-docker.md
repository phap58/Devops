<h1>CÁC CÂU LỆNH ĐƯỢC DÙNG TRONG DOCKER</H1>
<hr>
<h2>Nhóm lệnh thao tác với container</h2>
<ul>
<li>Câu lệnh <code>docker search</code>
<ul>
<li>Chức năng: tìm kiếm một images từ Docker Hub
<li>Cú pháp:

        docker search [OPTIONS] TERM
trong đó options bao gồm:
<table>
<tr>
<th>Options</th>
<th>Mặc định</th>
<th>Mô tả</th>
</tr>
<tr>
<th>--limit</th>
<th>25</th>
<th>Max number of search results</th>
</tr>
</table>

<li> Ví dụ:

        docker search debian
</ul>
<li>Câu lệnh docker pull:
<ul>
<li>Chức năng: Pull một image hoặc một repository từ registry
<li>Cú pháp:

        docker pull [OPTIONS] NAME[:TAG|@DIGEST]
trong đó options bao gồm:
<table>
<tr>
<th>Options</th>
<th>Mặc định</th>
<th>Mô tả</th>
</tr>
<tr>
<th>--all-tag, -a</th>
<th></th>
<th>Download tất cả tagged images trong repository</th>
</tr>
<tr>
<th>--disable-content-trust</th>
<th>true</th>
<th>Bỏ qua việc xác minh image
</th>
</tr>
</table>
<li> NAME là tên của image

<li>Ví dụ: Để pull một image từ Docker Hub. Ta thực hiện sử dụng câu lệnh:

          docker pull debian
kết quả:

        Using default tag: latest
        latest: Pulling from library/debian
        fdd5d7827f33: Pull complete
        : Pull complete
        Digest: sha256:e7d38b3517548a1c71e41bffe9c8ae6d6d29546ce46bf62159837aad072c90aa
        Status: Downloaded newer image for debian:latest
Docker images trên bao gồm 2 layer đó là: <Code> fdd5d7827f33</code> và <code>a3ed95caeb02</code>.
</ul>
<li>Câu lệnh <Code>docker create</code>
<ul>
<li>Chức năng: Tạo ra một container mới

<li>Cú pháp:

        docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
trong đó các options phổ biến bao gồm:
<table>
<tr>
<th>Options</th>
<th>Mặc định</th>
<th>Mô tả</th>
</tr>
<tr>
<th>--attach , -a</th>
<th></th>
<th>Attach to STDIN, STDOUT or STDERR</th>
</tr>
<tr>
<th>--expose</th>
<th></th>
<th>Để lộ ra một port hoặc một dải port - public port</th>
</tr>
<tr>
<th>--env , -e<th>
<th>Khai báo giá trị biến môi trường. Một vài image sẽ yêu cầu options này khi tạo ra container</th>
</tr>
<tr>
<th>--hostname , -h</th>
<th></th>
<th>Khai báo container host name</th>
</tr>
<tr>
<th>--ip</th>		
<th></th>
<th>Khai báo địa chỉ IPv4 cho container</th>
</tr>
<tr>
<th>--interactive , -i</th>
<th></th>
<th>Keep STDIN open even if not attached</th>
</tr>
<tr>
<th>
--link</th><th></th><th>		Khai báo tên container gắn kết với container sẽ tạo</th>
</tr><tr>
<th>--name</th><th></th><th>		Khai báo tên cho container</th></tr><tr><th>
--publish , -p</th><th></th><th>		Publish port(s) của container tới host</th></tr><tr><th>
--publish-all , -P	</th><th></th><th>	Publish tất cả exposed ports to ports ngẫu nhiên</th></tr><tr><th>
--rm</th><th></th><th>		Tự động xóa container khi thoát ra</th></tr><tr><th>
--runtime</th><th></th><th>		Khai báo runtime cho container</th></tr><tr><th>
--volume , -v	</th><th></th><th>	Gán một volume tới container</th></tr><tr><th>
--tty , -t	</th><th></th><th>	Allocate a pseudo-TTY</th></tr>
</table>
<li>Ví dụ: Để tạo ra một container từ image có tên là fedora và giao tiếp với cli của container. Sử dụng câu lệnh:

          docker create -t -i fedora bash
hoặc
          docker create -it fedora bash
kết quả:

          6d8af538ec541dd581ebc2a24153a28329acb5268abe5ef868c1f1a261221752
đây là ID của container được sử dụng thay cho tên (Có thể sử dụng một vài ký tự đầu của ID thay vì sử dụng toàn bộ)
</ul>
<li>Câu lệnh <code>docker cp</code>
<ul>
<li>Chức năng: Copy file/ folder giữa container và local filesystem.

<li>Cú pháp:

          docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
         docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
trong đó options bao gồm:
<table>
<tr>
<th>Options</th>
<th>Mặc định</th>
<th>Mô tả</th>
</tr>
<tr>
<th>--archive , -a</th>
<th></th>
<th>Archive mode (copy all uid/gid information)</th>
</tr>
<tr>
<th>--follow-link , -L</th>
<th></th>
<th>Always follow symbol link in SRC_PATH</th>
</tr>
</table>
nếu ký tự <code> -</code> được khai báo, ta có thể stream một file tar từ STDIN hoặc STOUT.

Khai báo <code>compassionate_darwin:/tmp/foo/myfile.txt</code> và <Code>compassionate_darwin:tmp/foo/myfile.txt</code> được xem là 2 khai báo giống nhau. Do <Code>docker cp</code> giả định đường dẫn tương đối là <code>/</code> (root)


</ul>
</ul>
