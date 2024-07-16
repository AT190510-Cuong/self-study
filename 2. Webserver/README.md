# 2. Webserver

![image](https://hackmd.io/_uploads/HkTejSXuC.png)

![image](https://hackmd.io/_uploads/HJrMoBmdR.png)

![image](https://hackmd.io/_uploads/Sy5chS7_C.png)

![image](https://hackmd.io/_uploads/SkBpnBmOA.png)

![image](https://hackmd.io/_uploads/SyBepHmd0.png)

- trên 1 webserver có thể cấu hình được nhiều site

![image](https://hackmd.io/_uploads/BknNjBmdC.png)

- webserver có thể rewrite url

![image](https://hackmd.io/_uploads/SkCIorQOC.png)

![image](https://hackmd.io/_uploads/SyKdsrQOR.png)

![image](https://hackmd.io/_uploads/rkKYjBmu0.png)

## cài đặt ứng dụng web wordpress

![image](https://hackmd.io/_uploads/SyVAFzzuR.png)

![image](https://hackmd.io/_uploads/HkA8ELGdC.png)

Mô hình ứng dụng web gồm 3 thành phần chính:

- webserver
- ứng dụng
- database

### webserver

- `sudo apt install apache2`

### database mysql

- `sudo apt install mysql-server`
- đăng nhập với user root và mật khẩu password `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';`

- tạo database wordpress
  ![image](https://hackmd.io/_uploads/rJJObPGd0.png)

- tạo 1 user mới quản lý wordpress `create user wpuser@localhost identified by 'password'`;

![image](https://hackmd.io/_uploads/HkuxVPMd0.png)

- gán toàn quyền dùng database wordpress cho user mới`grant all privileges on wordpress.* to wpuser@localhost;`

![image](https://hackmd.io/_uploads/Sk2oQwGu0.png)

### ứng dụng

cài mod-php (có thể cài các ứng dụng khác như mod-python, mod-perl)

- `sudo apt install php libapache2-mod-php php-mysql`

- tạo 1 file info.php

![image](https://hackmd.io/_uploads/BkQMHnMdA.png)

- webserver đã chạy được code php

![image](https://hackmd.io/_uploads/ByCkB2GuR.png)

#### cài đặt ứng dụng todolist

- tạo datable và user

![image](https://hackmd.io/_uploads/rkhaqhGOA.png)

- tạo table

![image](https://hackmd.io/_uploads/HyjLi3GOA.png)

- tạo 1 số giá trị

![image](https://hackmd.io/_uploads/Skg2j3zOR.png)

![image](https://hackmd.io/_uploads/S1l0s2zuA.png)

- tạo ứng dụng todolist kết nối database

![image](https://hackmd.io/_uploads/B1INnhzdR.png)

```php
<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}
```

![image](https://hackmd.io/_uploads/r1ryp2G_C.png)

#### cài wordpress

- https://www.youtube.com/watch?v=1dL1GtEoX5c&list=PLRz-2ltlXLUIkA8i8TC6pGYzzIWi5b7eP&index=35
- tải wordpress`wget https://wordpress.org/latest.zip`
- giải nén `unzip latest.zip`
- di chuyển toàn bộ wordpress sang documentroot `/var/www/html`
  ![image](https://hackmd.io/_uploads/r1KOHvzd0.png)

- cấu hình để chạy wordpress
  ![image](https://hackmd.io/_uploads/Syz2LPM_0.png)

- trong file wp-config.php sửa các biến môi trường
  ![image](https://hackmd.io/_uploads/HyeswvGOC.png)

![image](https://hackmd.io/_uploads/ByPsOPz_0.png)

![image](https://hackmd.io/_uploads/B1tl9PzOC.png)

![image](https://hackmd.io/_uploads/ryBN9wMdC.png)

- đăng nhập và mình vào được trang quản trị

![image](https://hackmd.io/_uploads/H1uD9Pf_0.png)

![image](https://hackmd.io/_uploads/BJMFiwMuC.png)

## cài đặt webserver chạy nhiều trang web

### apache

![image](https://hackmd.io/_uploads/By_mnwMuR.png)

- https://www.youtube.com/watch?v=1CDxpAzvLKY&t=799s
- https://httpd.apache.org/docs/current/vhosts/examples.html

![image](https://hackmd.io/_uploads/S1NIDsGdR.png)

- để tắt hiển thị version của webserver https://whitehat.vn/threads/cau-hinh-bao-mat-web-server-apache.17109/

- vô hiệu hóa trang web mặc định được cài đặt cùng với Apache. Điều này là bắt buộc nếu bạn không sử dụng tên miền tùy chỉnh, vì trong trường hợp này, cấu hình mặc định của Apache sẽ ghi đè lên máy chủ ảo của bạn

![image](https://hackmd.io/_uploads/B17jMnz_C.png)

- Với DirectoryIndexcác thiết lập mặc định trên Apache, một tệp được đặt tên index.htmlsẽ luôn được ưu tiên hơn một index.phptệp. Điều này hữu ích khi thiết lập các trang bảo trì trong các ứng dụng PHP, bằng cách tạo một index.htmltệp tạm thời chứa thông báo thông tin cho khách truy cập. Vì trang này sẽ được ưu tiên hơn trang index.php, nên sau đó nó sẽ trở thành trang đích cho ứng dụng. Sau khi bảo trì kết thúc, tệp index.htmlđược đổi tên hoặc xóa khỏi gốc tài liệu, đưa trang ứng dụng thông thường trở lại.

Trong trường hợp bạn muốn thay đổi hành vi này, bạn sẽ cần chỉnh sửa tệp /etc/apache2/mods-enabled/dir.confvà thay đổi thứ tự liệt index.phpkê tệp trong DirectoryIndexchỉ thị:

`sudo nano /etc/apache2/mods-enabled/dir.conf`

![image](https://hackmd.io/_uploads/B1HX42M_C.png)

```bash
<IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

- https://www.digitalocean.com/community/tutorials/how-to-configure-the-apache-web-server-on-an-ubuntu-or-debian-vps

![image](https://hackmd.io/_uploads/H1pj6vMOR.png)

- VD: nhiều website dùng 1 tên miền - 1 IP - 1 port https://www.youtube.com/watch?v=1CDxpAzvLKY&t=799s

```apache
<VirtualHost *:80>
        ServerAdmin webmaster@example.net
        ServerName example.net
        ServerAlias www.example.net
        DocumentRoot /var/www/html/example.net/public_html/
        ErrorLog /var/www/html/example.net/logs/error.log
        CustomLog /var/www/html/example.net/logs/access.log combined
</VirtualHost>
```

- bật 2 website trên webserver

![image](https://hackmd.io/_uploads/B1BS7pG_A.png)

- tạo 2 trang html của 2 website

![image](https://hackmd.io/_uploads/SkHJVazd0.png)

![image](https://hackmd.io/_uploads/BJ5fEafu0.png)

- trong burpsuit ta thấy

  - với Host: example.net thì webserver trả về website 1 ![image](https://hackmd.io/_uploads/rJ9wrafu0.png)
  - với Host: example.org thì webserver trả về website 2 ![image](https://hackmd.io/_uploads/ryvtSTMdC.png)

- VD: 1 website dùng 1 tên miền - 1 IP - nhiều port:

```apache
<VirtualHost *:8000>
        ServerName _
        ServerAlias project-dev   // phải trùng tên đã đăng kí trong /etc/hosts
        DocumentRoot /var/www/html/backend/public

        <Directory /var/www/html/backend/public/>
            Options Indexes FollowSymLinks MultiViews
            AllowOverride All
            Order allow,deny
            allow from all
            Require all granted
        </Directory>

        LogLevel debug
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combinedwq
</VirtualHost>

<VirtualHost *:80>
        ServerName _
        DocumentRoot /var/www/html/admin/dist

        <Directory /var/www/html/admin/dist>
            Options Indexes FollowSymLinks MultiViews
            AllowOverride All
            Order allow,deny
            allow from all
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combinedwq
</VirtualHost>

<VirtualHost *:3000>
        ServerName _

          ProxyPreserveHost On
          ProxyPass / http://localhost:3001/                   //phần chạy pm2 nè
          ProxyPassReverse / http://localhost:3001/             //phần chạy pm2 nè

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combinedwq
</VirtualHost>

```

### nginx

- tương tự apache có thể tham khảo thêm tại https://www.youtube.com/watch?v=1sdaPoXWQrw

## tham khảo

- https://www.digitalocean.com/community/tutorials/how-to-install-lamp-stack-on-ubuntu
- https://viblo.asia/p/cai-dat-server-voi-apache-tu-a-z-EbNVQ25p4vR
