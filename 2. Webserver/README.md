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

- Khi một máy tính muốn truy cập một trang web hoặc một tệp tin từ một máy chủ, nó gửi yêu cầu tới địa chỉ IP của máy chủ đó thông qua giao thức HTTP. Webserver sau đó nhận yêu cầu này, xử lý và tìm kiếm các tệp tin hoặc trang web tương ứng và trả về kết quả cho máy tính yêu cầu thông qua một trang web hoặc các tệp tin được truyền về qua mạng.

## Vai trò của Web Server

### 2.1 Xử lý yêu cầu từ client

- Tài nguyên tĩnh: (HTML, CSS, JavaScript, hình ảnh).
- Tài nguyên động: Chuyển tiếp yêu cầu đến backend hoặc Application
  Server để xử lý.

### 2.2 Cung cấp nội dung tĩnh

Trả về các tệp tĩnh như:
o HTML: Hiển thị giao diện người dùng.
o CSS: Định dạng giao diện.
o JavaScript: Xử lý logic phía client

- Điều này giúp giảm tải cho các thành phần backend, vì Web Server xử lý các
  yêu cầu cơ bản nhanh chóng.

### 2.3 Làm trung gian giữa client và backend

Proxy ngược (Reverse Proxy): Chuyển tiếp yêu cầu từ client đến backend
hoặc Application Server để xử lý các tài nguyên động.
• Cân bằng tải (Load Balancing): Phân phối yêu cầu đến nhiều server backend
để tối ưu hiệu suất và đảm bảo tính sẵn sàng.

### 2.4 Đảm bảo bảo mật

- Chứng chỉ SSL/TLS: Mã hóa kết nối để bảo vệ dữ liệu trao đổi giữa client
  và server.
- Quản lý quyền truy cập: Thiết lập cơ chế xác thực và phân quyền để bảo vệ
  tài nguyên.
- Tường lửa ứng dụng web (WAF): Phòng ngừa các cuộc tấn công như SQL
  Injection, Cross-Site Scripting (XSS), và DDoS

### 2.5 Quản lý phiên làm việc (Session Management)

- Lưu trữ thông tin phiên làm việc của người dùng, đảm bảo tính liên tục và
  đồng bộ giữa các lần gửi yêu cầu.

### 2.6 Tối ưu hóa hiệu suất

- Caching: Lưu trữ các kết quả xử lý tạm thời để giảm thời gian phản hồi
  trong các yêu cầu lặp lại.
- Compression: Giảm kích thước dữ liệu trả về (bằng Gzip hoặc Brotli) để
  tăng tốc độ tải trang.

### 2.7 Ghi log và theo dõi hoạt động

Ghi lại thông tin về các yêu cầu HTTP (địa chỉ IP, thời gian, trạng thái phản
hồi) để hỗ trợ:
o Phân tích hiệu suất.
o Xác định lỗi.
o Bảo trì hệ thống

### 2.8 Hỗ trợ các tính năng nâng cao

• Rewrite URL: Chuyển đổi các URL phức tạp thành các URL thân thiện với
người dùng và công cụ tìm kiếm.
• Redirect: Chuyển hướng yêu cầu từ một URL đến URL khác (ví dụ: từ
HTTP sang HTTPS).
• Virtual Hosting: Lưu trữ nhiều trang web trên cùng một máy chủ vật lý, sử
dụng các tên miền khác nhau.

## 3. Cách thức hoạt động của Web Server

### 3.1 Thiết lập kết nối

- Khi máy tính khách (client) muốn truy cập vào một trang
  web, nó gửi yêu cầu tới địa chỉ IP của máy chủ (server) thông qua một giao thức
  truyền tải siêu văn bản (HTTP). Quá trình này thường bắt đầu bằng việc thiết lập
  kết nối TCP/IP giữa client và server

### 3.2 Xử lý yêu cầu

### 3.3 Tìm kiếm tài nguyên

- Sau khi phân tích yêu cầu, web server sẽ tìm kiếm và
  truy cập tài nguyên tương ứng. Điều này có thể bao gồm đọc tệp tin từ hệ thống tệp
  của máy chủ hoặc tương tác với cơ sở dữ liệu để lấy thông tin

### 3.4 Xây dựng response: Dựa trên yêu cầu và tài nguyên đã tìm kiếm, web server

- sẽ xây dựng một response để trả về cho máy tính khách. Response này thường bao
  gồm một mã trạng thái (status code) để chỉ ra thành công hay thất bại của yêu cầu,
  các thông tin header như loại nội dung, kích thước tệp tin, và nội dung thực tế được
  trả về.

### 3.5 Trả về response: Cuối cùng, web server sẽ gửi response được xây dựng trở lại

- cho máy tính khách qua mạng. Máy tính khách nhận response và hiển thị nội dung
  tương ứng cho người dùng.
  Quá trình này diễn ra liên tục và web server có thể xử lý đồng thời nhiều yêu cầu
  từ các máy tính khách khác nhau\*\*\*\*

## 4. Các Web Server phổ biến

- 4.1 Apache HTTP Server:
- 4.2 Nginx:
- 4.3 Microsoft Internet Information Services (IIS):
- Ngoài ra, còn nhiều web server khác như LiteSpeed, Cherokee, IBM HTTP Server,
  thậm chí cả các web server tích hợp trong các framework như Flask và Express.js.

## WEB APPLICATION

### 2. Vai trò Web Application

#### 2.3 Tích hợp và xử lý dữ liệu:

- Kết nối với cơ sở dữ liệu để lưu trữ, truy xuất, và quản lý dữ liệu.
- Xử lý logic nghiệp vụ để đáp ứng nhu cầu sử dụng cụ thể của người dùng.

#### 2.4 Đa nền tảng:

- Hoạt động trên mọi thiết bị có trình duyệt (PC, smartphone, tablet) mà không phụ
  thuộc vào hệ điều hành.

#### 3.3 Xử lý tại Web Application (Backend):

Web Application xử lý logic nghiệp vụ, thực hiện các tác vụ như:
o Lấy dữ liệu từ cơ sở dữ liệu.
o Tính toán hoặc xử lý yêu cầu nghiệp vụ.
o Tạo nội dung động (Dynamic Content)

#### 3.4 Trả phản hồi về trình duyệt:

• Web Application gửi kết quả đến Web Server, và Web Server chuyển phản hồi này đến trình duyệt.
• Trình duyệt hiển thị nội dung cho người dùng

### 4.4 Dựa trên công nghệ backend

• Full-stack Web Applications:
o Sử dụng cả backend và frontend frameworks (ví dụ: MERN stack -
MongoDB, Express, React, Node.js).
• Headless Web Applications:
o Backend chỉ cung cấp API, frontend xử lý hiển thị độc lập.

### Mối quan hệ giữa Web Server và Web Application

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

### Virtual host

- `Name-Based Virtual Hosting`: Phương pháp này chỉ dựa vào HTTP Host headerđể phân biệt giữa các trang web. Đây là phương pháp phổ biến và linh hoạt nhất vì không yêu cầu nhiều địa chỉ IP. Phương pháp này tiết kiệm chi phí, dễ thiết lập và hỗ trợ hầu hết các máy chủ web hiện đại. Tuy nhiên, phương pháp này yêu cầu máy chủ web phải hỗ trợ dựa trên tên virtual hostingvà có thể có những hạn chế với một số giao thức như SSL/TLS.
- `IP-Based Virtual Hosting`: Loại lưu trữ này gán một địa chỉ IP duy nhất cho mỗi trang web được lưu trữ trên máy chủ. Máy chủ xác định trang web nào sẽ phục vụ dựa trên địa chỉ IP mà yêu cầu được gửi đến. Nó không dựa vào Host header, có thể được sử dụng với bất kỳ giao thức nào và cung cấp khả năng cô lập tốt hơn giữa các trang web. Tuy nhiên, nó yêu cầu nhiều địa chỉ IP, có thể tốn kém và ít khả năng mở rộng hơn.
- `Port-Based Virtual Hosting`: Các trang web khác nhau được liên kết với các cổng khác nhau trên cùng một địa chỉ IP. Ví dụ, một trang web có thể truy cập được trên cổng 80, trong khi một trang web khác trên cổng 8080. Port-based virtual hostingcó thể được sử dụng khi địa chỉ IP bị giới hạn, nhưng không phổ biến hoặc thân thiện với người dùng như name-based virtual hostingvà có thể yêu cầu người dùng chỉ định số cổng trong URL.

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
