# 6. Mod Security

## Khái niệm

- Mod Security là một module tường lửa có thể tích hợp với các Web Application Server (máy chủ ứng dụng web) như Apache, IIS, Nginx cho phép phân tích và ghi nhật ký các luồng dữ liệu HTTP/S.Với sự đóng góp từ dự án ModSecurity Core Rule Set của tổ chức OWASP đã giúp ModSecurity trở nên mạnh mẽ và linh động hơn trong việc phân tích các hành vi có nguy cơ xâm hại an ninh ứng dụng web.
- Mod Security đứng trước Web Server, làm nhiệm vụ như một firewall để kiểm soát truy cập vào ra Web Server. Các thông tin đi từ bên ngoài vào và bên trong ra sẽ được kiểm soát chặt chẽ để tránh những thông tin có thể gây hại cho Web Server hay là việc rò rỉ các thông tin đặc biệt từ Web Server đến Client.

![image](https://hackmd.io/_uploads/HkEO3gUOA.png)

Mod Security giúp:

- Understanding of the HTTP protocol: ModSecurity là web application firewall nên nó có khả năng hiểu được HTTP protocol. ModSecurity có khả năng càn lọc dựa trên các thông tin ở HTTP header hay có thể xem xét đến từng parameters hay cookies của các requests…
- POST payload analysis: ngoài việc càn lọc dựa trên HTTP header, ModSecurity có thể dựa trên nội dung (payload) của POST request.
- Audit logging: mọi request đều có thể được ghi lại (bao gồm cả POST) để người quản trị có thể theo dõi nếu cần.

![image](https://hackmd.io/_uploads/ryxzmchu0.png)

## Vai trò

- Giám sát bảo mật ứng dụng và kiểm soát truy cập theo thời gian thực

  - Về cơ bản, ModSecurity cung cấp cho bạn quyền truy cập vào luồng lưu lượng HTTP, theo thời gian thực, cùng với khả năng kiểm tra luồng đó. Điều này đủ để giám sát bảo mật theo thời gian thực. Có một chiều hướng bổ sung về những gì có thể thông qua cơ chế lưu trữ liên tục của ModSecurity, cho phép bạn theo dõi các thành phần hệ thống theo thời gian và thực hiện tương quan sự kiện. Bạn có thể chặn một cách đáng tin cậy, nếu bạn muốn, vì ModSecurity sử dụng bộ đệm yêu cầu và phản hồi đầy đủ.

- Không thể truy cập vào một số tiêu đề phản hồi
  - Do cách thức hoạt động của Apache, các tiêu đề phản hồi Servervà Datetiêu đề phản hồi là vô hình đối với ModSecurity; chúng không thể được kiểm tra hoặc ghi lại

## cách thức hoạt động

![image](https://hackmd.io/_uploads/B1OeIkg4ye.png)

![image](https://hackmd.io/_uploads/rysG4elVyl.png)

1. Giai đoạn tiêu đề yêu cầu Giai đoạn tiêu đề yêu cầu:
   Apache xử lý các quy tắc trong giai đoạn này ngay sau khi hoàn thành việc đọc tiêu đề yêu cầu (giai đoạn sau đọc-yêu cầu). Nội dung yêu cầu chưa được đọc tại thời điểm này, vì vậy không phải tất cả các tham số yêu cầu đều có sẵn tại thời điểm này. Nếu bạn cần chạy quy tắc sớm (trước khi Apache thực hiện điều gì đó với yêu cầu), trước khi nội dung yêu cầu được đọc, bạn cần quyết định xem nội dung yêu cầu có nên được lưu vào bộ đệm hay không hoặc quyết định cách đặt quy tắc ở giai đoạn này (ví dụ: liệu Phân tích nó thành XML).
2. Giai đoạn nội dung yêu cầu Giai đoạn nội dung yêu cầu:
   Giai đoạn nội dung yêu cầu là giai đoạn phân tích đầu vào chung, trong đó hầu hết các quy tắc hướng ứng dụng được đặt. Ở giai đoạn này, tất cả các tham số yêu cầu đều có thể được nhận, tất nhiên, tiền đề này là nội dung yêu cầu đã được đọc. Ở giai đoạn này ModSecurity hỗ trợ ba loại mã hóa trong giai đoạn nội dung yêu cầu:

- `application/x-www-form-urlencoded` được sử dụng để truyền dữ liệu biểu mẫu
- `multipart/form-data` để tải lên tập tin
- `text/xml` được sử dụng để truyền dữ liệu XML.
  Hầu hết các ứng dụng web không sử dụng các bảng mã khác

3. Tiêu đề phản hồi pha Giai đoạn tiêu đề phản hồi:
   Giai đoạn này xảy ra trước khi tiêu đề phản hồi được gửi lại cho máy khách. Nếu bạn muốn kiểm tra phản hồi trước đó và liệu bạn có muốn sử dụng tiêu đề phản hồi để quyết định có lưu nội dung phản hồi vào bộ nhớ đệm hay không, bạn có thể định cấu hình quy tắc cho giai đoạn này. Cần lưu ý rằng một số mã trạng thái phản hồi (chẳng hạn như 404) được xử lý sớm trong chu kỳ yêu cầu Apache, do đó việc truy cập như vậy không thể kích hoạt các quy tắc ModSecurity. Ngoài ra, có một số tiêu đề phản hồi được Apache thêm vào trong các hook sau này (chẳng hạn như ngày, máy chủ và kết nối) mà ModSecurity cũng không thể kích hoạt hoặc kiểm tra. Điều này phải được cấu hình trong cài đặt tác nhân hoặc ở giai đoạn 5 (ghi nhật ký).
4. Giai đoạn nội dung phản hồi Giai đoạn nội dung phản hồi:
   Giai đoạn nội dung phản hồi là giai đoạn phân tích đầu ra chung. Nội dung phản hồi tại thời điểm này đáng lẽ phải được lưu vào bộ đệm, sau đó chạy quy tắc để kiểm tra nội dung phản hồi. Ở giai đoạn này, HTML gửi đi có thể được kiểm tra để xác định xem có bất kỳ rò rỉ thông tin, thông báo lỗi hoặc văn bản xác thực không thành công hay không.
5. Giai đoạn ghi nhật ký Giai đoạn ghi nhật ký:
   Giai đoạn này chạy trước khi quá trình ghi nhật ký diễn ra. Các quy tắc bước vào giai đoạn này chỉ ảnh hưởng đến cách thực hiện ghi nhật ký. Giai đoạn này có thể được sử dụng để kiểm tra các thông báo lỗi được Apache ghi lại. Nhưng kết nối không thể bị từ chối/chặn ở giai đoạn này vì đã quá muộn. Giai đoạn này cũng cho phép kiểm tra các tiêu đề phản hồi khác không có sẵn trong giai đoạn 3 hoặc giai đoạn 4. Cần lưu ý rằng ở giai đoạn này không kế thừa thao tác từ chối/chặn vào quy tắc, vì bản thân đây đã là lỗi cấu hình.

![image](https://hackmd.io/_uploads/SkQnuB1E1x.png)

Modsecurity có cơ chế hoạt động như một cỗ máy IDPS. Công cụ này thực hiện quá trình phát hiện các xâm nhập lạ vào website.

ModSecurity bắt đầu từ việc giám sát luồng dữ liệu HTTP với các yêu cầu được gửi tới Server. Sau đó, Modsecurity sẽ phân tích các yêu cầu để tìm ra sự cố bất thường.

Những bất thường này thường vi phạm chính sách an ninh của các web server. Khi đó, Modsecurity sẽ giúp ngăn chặn hoặc loại bỏ các yêu cầu để bảo vệ hệ thống web.

Có hai phương pháp để Modsecurity thực hiện ngăn chặn các tấn công. Đó là dựa vào mẫu được lập trình sẵn và dựa vào các dấu hiệu bất thường. Việc phát hiện lỗi từ luồng dữ liệu của Modsecurity trở nên đơn giản hơn, nhanh chóng hơn.

Đối với các lỗi được xác định bất thường, Modsecurity sẽ tập hợp và đánh giá theo mức độ. Lỗi càng cao đồng nghĩa với mức độ đe dọa an ninh càng lớn. Khi đó, công cụ sẽ chặn hoặc loại bỏ các yêu cầu được gửi đến.

![image](https://hackmd.io/_uploads/HJZpApJ4Je.png)

![image](https://hackmd.io/_uploads/B1JQxel4Jl.png)

- Modsecurity hoạt động trên 5 pha:

| Phase number | Phase name       | Phase occurs                                                                                         |
| ------------ | ---------------- | ---------------------------------------------------------------------------------------------------- |
| 1            | REQUEST_HEADERS  | Pha này thực hiện sau khi mà Apache đọc được phần headers của HTTP request                           |
| 2            | REQUEST_BODY     | Sau khi phần body của 1 HTTP request được đọc thì Mod security sẽ áp các luật của mình vào phần body |
| 3            | RESPONSE_HEADERS | Pha này thực hiện trước khi 1 response headers được gửi tới cho client                               |
| 4            | RESPONSE_BODY    | Pha này được thực hiện khi 1 response body được gửi tới cho phía client                              |
| 5            | LOGGING          | Pha này thực hiện kiểm soát file log                                                                 |

|

- `Phase Request Header (phase: 1)`: rule được đặt tại đây sẽ được thực hiện ngay sau khi Apache đọc request header, lúc này phần request body vẫn chưa được đọc.
- `Phase Request Body (phase: 2)`: đây là thời điểm các thông tin chức năng chung đưa vào vào được phân tích và xem xét, các rule mang tính application-oriented thường được đặt ở đây. Ở thời điểm này bạn đã nhận đủ các request argument và phần request body đã được đọc. Modsecurity hỗ trợ ba loại mã hoá request body
  - `application/x-www-form-urlencoded` dùng để truyền form dữ liệu
  - `multipart/form-data` dùng để truyền file
  - `text/xml` dùng để phân tich dữ liệu XML
- `Phase Response Header (phase: 3)`: đây là thời điểm ngay sau khi phần response header được gửi trả về cho client. Bạn đặt rule ở đây nếu muốn giám sát quá trình sau khi phần response được gửi đi.
- `Phase Response Body (phase: 4)`: đây là thời điểm bạn muốn kiểm tra những dữ liệu HTML gửi trả về
- `Logging`: đây là thời điểm các hoạt động log được thực hiện, các rules đặt ở đây sẽ định rõ việc log sẽ như thế nào, nó sẽ kiểm tra các error message log của Apache. Đây cung là thời điểm cuối cùng để bạn chặn các connection không mong muốn, kiểm tra các response header mà bạn không thể kiểm tra ở phase 3 và phase 4.

## Cấu hình lại Apache để chạy trang web trên port 80

- mật khẩu đăng nhập database và wordpress lần lượt là :

`password`
![image](https://hackmd.io/_uploads/HypCYH6Qyg.png)

`SM$SrPdrAji6fSo5E4`
![image](https://hackmd.io/_uploads/Sy0yqSpXkl.png)

![image](https://hackmd.io/_uploads/S1d498pm1x.png)

- đăng nhập với user root và tạo database

![image](https://hackmd.io/_uploads/BJFARHamJx.png)

- tạo user

![image](https://hackmd.io/_uploads/Bkg218pmke.png)

- gán quyền `grant all privileges on todolist.* to todoapp@localhost ;`

![image](https://hackmd.io/_uploads/HJ8SxUp7ye.png)

- vào database tạo data

![image](https://hackmd.io/_uploads/S11Tg8am1l.png)

![image](https://hackmd.io/_uploads/Hyt4W8T7Jg.png)

![image](https://hackmd.io/_uploads/r1ZOPIamyg.png)

- đang bật cấu hình virtul host với 2 site sau:

![image](https://hackmd.io/_uploads/Skea_L671g.png)

Tắt example.net.conf và example.org.conf trong thư mục sites-enabled bằng cách sử dụng lệnh sau:

```bash
sudo a2dissite example.net.conf
sudo a2dissite example.org.conf
```

![image](https://hackmd.io/_uploads/H16bFITmkx.png)

- Kích hoạt 000-default.conf

```bash
sudo a2ensite 000-default.conf
```

![image](https://hackmd.io/_uploads/SkK_YIpQyl.png)

- và đã về được cấu hình mặc định

![image](https://hackmd.io/_uploads/Bk1AFLamJx.png)

- tạo 2 file: 1 bị sql, 1 ko bị sql và phải cấp quyền cho nó chạy

![image](https://hackmd.io/_uploads/Skxnt_aQkg.png)

## code file `sqli_rawquery.php`

```php
<?php
$host = "localhost";
$user = "todoapp";
$pass = "123456";
$dbname = "todolist";

// Kết nối cơ sở dữ liệu
$conn = mysqli_connect($host, $user, $pass, $dbname);

// Kiểm tra kết nối
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}

// Kiểm tra nếu form được submit
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Lấy thông tin từ form
    $username = $_POST['username'];
    $password = $_POST['password'];

    // Câu lệnh SQL không an toàn
    $query = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";
    $result = mysqli_query($conn, $query);

    // Kiểm tra kết quả
    if (mysqli_num_rows($result) > 0) {
        echo "Đăng nhập thành công!<br>";
        while ($row = mysqli_fetch_assoc($result)) {
            echo "Xin chào, " . $row['username'] . "!";
        }
    } else {
        echo "Sai tên đăng nhập hoặc mật khẩu.";
    }
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Đăng Nhập</title>
</head>
<body>
    <h1>Form Đăng Nhập</h1>
    <form action="sqli_rawquery.php" method="post">
        <label for="username">Tên đăng nhập:</label><br>
        <input type="text" id="username" name="username" required><br><br>

        <label for="password">Mật khẩu:</label><br>
        <input type="password" id="password" name="password" required><br><br>

        <button type="submit">Đăng Nhập</button>
    </form>
</body>
</html>

```

- đăng nhập ko thành công sẽ hiện `Sai tên đăng nhập hoặc mật khẩu.`

![image](https://hackmd.io/_uploads/rknioOaXyl.png)

- đăng nhập thành công sẽ hiện `Đăng nhập thành công!Xin chào, cuong!`

![image](https://hackmd.io/_uploads/rJumhOTmJx.png)

- thấy trigger sqli thành công

![image](https://hackmd.io/_uploads/rJoAhuamyx.png)

## code file `sqli_prepare.php`

```php
<?php
$host = "localhost";
$user = "todoapp";
$pass = "123456";
$dbname = "todolist";

// Kết nối cơ sở dữ liệu
$conn = mysqli_connect($host, $user, $pass, $dbname);

// Kiểm tra kết nối
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}

// Kiểm tra nếu form được submit
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Lấy thông tin từ form
    $username = $_POST['username'];
    $password = $_POST['password'];

    // Sử dụng prepared statement để ngăn ngừa SQL Injection
    $stmt = $conn->prepare("SELECT * FROM users WHERE username = ? AND password = ?");

    // Liên kết tham số với câu lệnh SQL
    $stmt->bind_param("ss", $username, $password);

    // Thực thi câu lệnh
    $stmt->execute();

    // Lấy kết quả từ truy vấn
    $result = $stmt->get_result();

    // Kiểm tra kết quả
    if (mysqli_num_rows($result) > 0) {
        echo "Đăng nhập thành công!<br>";
        while ($row = mysqli_fetch_assoc($result)) {
            echo "Xin chào, " . $row['username'] . "!";
        }
    } else {
        echo "Sai tên đăng nhập hoặc mật khẩu.";
    }
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Đăng Nhập</title>
</head>
<body>
    <h1>Form Đăng Nhập</h1>
    <form action="sqli_prepare.php" method="post">
        <label for="username">Tên đăng nhập:</label><br>
        <input type="text" id="username" name="username" required><br><br>

        <label for="password">Mật khẩu:</label><br>
        <input type="password" id="password" name="password" required><br><br>

        <button type="submit">Đăng Nhập</button>
    </form>
</body>
</html>
```

- thấy không trigger được sqli

![image](https://hackmd.io/_uploads/rJtaCOTmye.png)

## WAF - modsecurity trên apache

![image](https://hackmd.io/_uploads/HJ4Prxl41e.png)

- thực hiện kiểm tra lưu lượng truy cập đến và đi khỏi ứng dụng web, cung cấp khả năng chống lại các cuộc tấn công Layer 7 như SQL Injection, LFI, XSS,… dựa trên HTTP request và response khác với các Firewall khác như Iptables, UFW, Firewalld,.. hoạt động chủ yếu trên Layer 3, 4, Modsecurity cho phép theo dõi lưu lượng HTTP, ghi log và phân tích realtime….
- Modsecurity hỗ trợ nhiều webserver như Nginx, Apache, IIS
- ModSecurity là application firewall thuộc loại rules-based, nghĩa chúng ta cần thiết lập các luật (rules) để ModSecurity hoạt động. Các rules này được thể hiện dưới dạng các dẫn hướng (directive) và có thể đặt trực tiếp trong file cấu hình Apache (thông thường là httpd.conf).
  - Ngoài ra có thể đặt các cấu hình này vào một file riêng, chẳng hạn ModSecurity.conf trong thư mục conf.d và sau đó chúng ta cần thêm vào httpd.conf
  - Include conf.d/ModSecurity.conf(mặc định trong httpd.conf đã có dòng include conf.d/\*.conf với dòng này nó sẽ thực hiện tất cả các file có phần mở rộng là .conf)

### Cài đặt

```bash
sudo apt update -y
sudo apt install libapache2-mod-security2
```

![image](https://hackmd.io/_uploads/BJXW-tpXyl.png)

### cấu hình Modsecurity

```bash
cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
```

![image](https://hackmd.io/_uploads/H15ZXFpmye.png)

- thấy tải xong rồi reload apache2 vẫn bị sqli

![image](https://hackmd.io/_uploads/SkvjEtTm1l.png)

- cấu hình modsecurity , chuyển SecRuleEngine -> DetectionOnly thành On - Tắt hoặc bật hoạt động của các Rule
  Theo mặc định thì rule engine bị disable. Để kích hoạt ModSecurity ta cần thêm chỉ thị sau vào file cấu hình
  SecRuleEngine On - Dẫn hướng này dùng để điều khiển rule engine, chúng ta có thể sử dụng các tuỳ chọn là On, Off hoặc DynamicOnly. - `Off`: Vô hiệu hoá ModSecurity - `DetectionOnly`: Khi nó phù hợp một luật nào đó thì nó cũng không thực hiện bất kì action nào (nó rất có ích trong trường hợp muốn test một luật nào đó mà không muốn nó block bất kì request nào có vấn đề với luật) - `On` : Các rules của ModSecurity được áp dụng cho tất cả các nội dung

```bash
sudo nano /etc/modsecurity/modsecurity.conf
```

![image](https://hackmd.io/_uploads/rJHZ-1CXyl.png)

- cài đặt bộ luật CoreRuleSet cho ModSecurity

```bash
cd /etc/modsecurity/
sudo wget https://github.com/coreruleset/coreruleset/archive/refs/tags/v3.3.2.tar.gz
sudo tar -xzf v3.3.2.tar.gz
sudo mv coreruleset-3.3.2/crs-setup.conf.example /etc/modsecurity/crs-setup.conf
sudo mv coreruleset-3.3.2/rules/ /etc/modsecurity/
sudo rm modsecurity.conf-recommended
```

![image](https://hackmd.io/_uploads/Sky4zkCmJe.png)

![image](https://hackmd.io/_uploads/H1amnwCX1x.png)

- sửa đổi nội dung file cấu hình modSecurity của apache

```bash
sudo nano /etc/apache2/mods-enabled/security2.conf
```

![image](https://hackmd.io/_uploads/r1lFRwRQye.png)

- nội dung cấu hình cũ

![image](https://hackmd.io/_uploads/SJi33P0X1g.png)

```bash
<IfModule security2_module>
        # Default Debian dir for modsecurity's persistent data
        SecDataDir /var/cache/modsecurity

        # Include all the *.conf files in /etc/modsecurity.
        # Keeping your local configuration in that directory
        # will allow for an easy upgrade of THIS file and
        # make your life easier
        IncludeOptional /etc/modsecurity/*.conf

        # Include OWASP ModSecurity CRS rules if installed
        IncludeOptional /usr/share/modsecurity-crs/*.load
</IfModule>
```

- nội dung sửa đổi

![image](https://hackmd.io/_uploads/SyZwZOCmyx.png)

```bash
<IfModule security2_module>
        # Default Debian dir for modsecurity's persistent data
        SecDataDir /var/cache/modsecurity

        # Include all the *.conf files in /etc/modsecurity.
        # Keeping your local configuration in that directory
        # will allow for an easy upgrade of THIS file and
        # make your life easier
        IncludeOptional /etc/modsecurity/*.conf
        Include /etc/modsecurity/rules/*.conf

        # Include OWASP ModSecurity CRS rules if installed
        # IncludeOptional /usr/share/modsecurity-crs/*.load
</IfModule>
```

- lưu file thấy vẫn chưa chặn được SQLI

![image](https://hackmd.io/_uploads/r1i9AwCmJl.png)

```bash
root@cuong-virtual-machine:/etc/apache2/sites-enabled# systemctl status apache2
× apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: failed (Result: exit-code) since Thu 2024-12-05 07:09:30 +07; 34s ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 63954 ExecStart=/usr/sbin/apachectl start (code=exited, status=1/FAILURE)
        CPU: 257ms

Thg 12 05 07:09:30 cuong-virtual-machine systemd[1]: Starting The Apache HTTP Server...
Thg 12 05 07:09:30 cuong-virtual-machine apachectl[63957]: AH00526: Syntax error on line 829 of /etc/modsecurity/crs/crs-setup.conf:
Thg 12 05 07:09:30 cuong-virtual-machine apachectl[63957]: ModSecurity: Found another rule with the same id
Thg 12 05 07:09:30 cuong-virtual-machine apachectl[63954]: Action 'start' failed.
Thg 12 05 07:09:30 cuong-virtual-machine apachectl[63954]: The Apache error log may have more information.
Thg 12 05 07:09:30 cuong-virtual-machine systemd[1]: apache2.service: Control process exited, code=exited, status=1/FAILURE
Thg 12 05 07:09:30 cuong-virtual-machine systemd[1]: apache2.service: Failed with result 'exit-code'.
Thg 12 05 07:09:30 cuong-virtual-machine systemd[1]: Failed to start The Apache HTTP Server.
Thg 12 05 07:09:42 cuong-virtual-machine systemd[1]: apache2.service: Unit cannot be reloaded because it is inactive.
root@cuong-virtual-machine:/etc/apache2/sites-enabled# systemctl start apache2
Job for apache2.service failed because the control process exited with error code.
See "systemctl status apache2.service" and "journalctl -xeu apache2.service" for details.
root@cuong-virtual-machine:/etc/apache2/sites-enabled#
```

![image](https://hackmd.io/_uploads/HyF61u0XJx.png)

- Apache không khởi động được do gặp lỗi cú pháp trong tệp cấu hình /etc/modsecurity/crs/crs-setup.conf tại dòng 829. Cụ thể, lỗi cho biết rằng có một rule (quy tắc) trong ModSecurity bị trùng ID với một quy tắc khác.
- Kiểm tra xem ID 900990 có bị trùng không: `grep "id:900990" /etc/modsecurity/ -r`

![image](https://hackmd.io/_uploads/Bk21WOC71l.png)

Sửa ID thành một giá trị duy nhất:

- Nếu ID này bị trùng, bạn có thể thay đổi nó thành một số khác không bị trùng, ví dụ: 900991.

```bash
SecAction \
    "id:900991,\
    phase:1,\
    nolog,\
    pass,\
    t:none,\
    setvar:tx.crs_setup_version=332"
```

- Kiểm tra lại cấu hình Apache: `apachectl configtest`

![image](https://hackmd.io/_uploads/rJWCbdAmye.png)

![image](https://hackmd.io/_uploads/SkZlfu0Xyl.png)

- khởi động lại apache thấy WAF đã hoặt động và chặn các lưu lượng trái phép từ SQLI

![image](https://hackmd.io/_uploads/By_SzOA71e.png)

- khi modsecurity được bặt chúng ta sẽ nhận được kết quả như sau

![image](https://hackmd.io/_uploads/BkK2K_07kx.png)

![image](https://hackmd.io/_uploads/SkFXfdR7ke.png)

![image](https://hackmd.io/_uploads/Hyu2pYCQkx.png)

- request này bị cấm và phía server không xử lý request này

- vào đọc log của apachee để xem request đã bị chặn thế nào

```bash
cd /var/log/apache2/
cat error.log
```

![image](https://hackmd.io/_uploads/BkRH9dRQye.png)

![image](https://hackmd.io/_uploads/ryQ6hu07ke.png)

- Modsecurity sử dụng luật `/etc/modsecurity/rules/REQUEST-920-PROTOCOL-ENFORCEMENT.conf` để phát hiện tấn công SQLi và chặn nó
- detected SQLi using libinjection with fingerprint `/etc/modsecurity/rules/REQUEST-942-APPLICATION-ATTACK-SQLI.conf`
- và cuối cùng đánh giá điểm của cuộc tấn công trong trường hợp này điểm đánh giá là 8

- `SecDefaultAction`
  Dùng để tạo các action mặc định. Khi tạo 1 luật mà không chỉ rõ hành động cho luật đó nó sẽ thực hiện hành động mặc định

Ví dụ:

```php
SecDefaultAction"phase:2,deny,log,status:403"
```

ở đây:

- Phase:2:action này được xử lý ở phase thứ 2(Phase Request Body).
- Deny:Chặn request.
- Log: có ghi lại log
- Status:403:đặt status thông báo là 403.

- với một cuộc tấn công XSS khác

![image](https://hackmd.io/_uploads/B1C_yKAXkg.png)

![image](https://hackmd.io/_uploads/B15vyYRXJg.png)

- tắt WAF

```bash
nano /etc/modsecurity/modsecurity.conf
```

Tìm dòng:

```apache
SecRuleEngine On
```

Đổi thành:

```apache
SecRuleEngine Off
```

![image](https://hackmd.io/_uploads/ByavEd0Qkg.png)

- sau đó restart apache với `sudo systemctl restart apache2`
- thấy được SQLI vẫn trigger thành công

![image](https://hackmd.io/_uploads/S14iNOCm1e.png)

### Rules

![image](https://hackmd.io/_uploads/By2qxleV1g.png)

```php
SecRule REQUEST_FILENAME "@endsWith /admin/config/services/rss-publishing" \
    "id:9001216,\
    phase:2,\
    pass,\
    nolog,\
    ctl:ruleRemoveTargetByTag=OWASP_CRS;ARGS:feed_description,\
    ver:'OWASP_CRS/3.2.0'"
```

- Cấu trúc cơ bản của một rules:

```php
SecRule VARIABLES OPERATOR [ACTIONS]
```

- Dưới đây là một ví dụ về các sử dụng biến ARGS

```php
SecRule ARGS dirty.
```

- (dirty chuỗi ký tự đại diện cho các giá trị mà ARGS có thể nhận)
  Có thể dùng 1 hay nhiều variables

```php
SecRule ARGS|REQUEST_HEADERS:User-Agent dirty
```

- Collections
  Một variables có thể bao gồm 1 hay nhiều phần dữ liệu. Khi variable có nhiều hơn 1 giá trị thì ta gọi nó là collection
  Ví dụ: với variable ARGS ta có 2 thông số p, và q

```php
SecRule ARGS:p dirty
SecRule ARGS:q dirty
```

#### Toán tử (Operators)

- Xác định phương pháp và so sánh khớp dữ liệu để kích hoạt Action.

```php!
SecRule ARGS "@rx dirty"
```

- Sử dụng !@ để chỉ ra một phủ định của operator

```php!
SecRule &ARGS "!@rx ^0$"
```

- `@rx`: kiểm tra xem một chuỗi có khớp với một biểu thức chính quy hay không.
- `@eq`: kiểm tra xem hai chuỗi có bằng nhau hay không.
- `@contains`: kiểm tra xem một chuỗi có chứa một chuỗi con hay không.
- `@pm`: kiểm tra xem một chuỗi có chứa một chuỗi khác theo kiểu phân biệt chữ hoa chữ thường hay không.

#### Actions

- Khi request vi phạm một rule nào đó thì ModSecurity sẽ thực thi một hành động (action). Khi action không được chỉ rõ trong rule thì rule đó sẽ sử dụng default action . Có 3 loại actions:

  - `Primary actions`: sẽ quyết định cho phép request tiếp tục hay không. Mỗi rule chỉ có một primary action
    - `deny`: Request sẽ bị ngắt, ModSecurity sẽ trả về HTTP status code 500 hoặc là status code của bạn thiết lập trong chỉ thị status:
    - `pass`: Cho phép request tiếp tục được xử lý ở các rules tiếp theo
    - `allow`: Cho phép truy cập ngay lập tức và bỏ qua các phases khác (trừ phases logging). Nếu muốn chỉ cho qua phase hiện tại thì cần chỉ rõ allow:phase Khi đó sẽ vẫn được kiểm tra bởi các luật tại các phases sau. Chỉ cho phép truy cập tới các request
    - `phases`: allow:request, nó sẽ cho qua phase 1,2 và vẫn kiểm tra ở phase 3 trở đi
    - `redirect`: Redirect một request đến một url nào đó.
  - `Secondary actions` sẽ bổ sung cho Primary actions, một rule có thể có nhiều Secondary actions
    - `status`: n khi một Request vi phạm một rule nào đó thì ModSecurity có thể trả về các HTTP status code n thay vì status code 500 mặc định.
    - `exec`: thực thi một lệnh nào đó nếu một request vi phạm
    - `log`: ghi log những request vi phạm rule
    - `nolog`: không ghi log
    - `pause`: n ModSecurity sẽ đợi một thời gian n ms rồi mới trả về kết quả.
    - `Flow action` ảnh hưởng tới thứ tự các rule được xử lý
    - `chain`: kết nối 2 hay nhiều rules lại với nhau

- Ví dụ:

```php
SecRule REQUEST_HEADERS:User-agent “Red Bullet”“chain,deny”

SecRule REMOTE_ADDR “^192\.168\.1\.” Bullet” “chain,deny” SecRule REMOTE_ADDR “^192\.168\.1\.”
```

skipnext:n ModSecurity sẽ bỏ qua n rules theo sau nó

```php
SecRule REQUEST_HEADERS:User-agent“Red Bullet”“deny” skipnext:3
```

### Core Rule Set và một số cách phòng chống một số lỗi thường có trên apache:

#### Core Rule Set (CRS):

- CRS là một hệ thống bao gồm các tập luận đã được xây dựng sẵn dựa trên các lỗi thường có trên ứng dụng Web như XSS, SQL injection…
- Việc dùng core ruset sẽ làm cho người quản trị đơn giản hơn trong việc xây dựng các rules , vì core rule set đã được xây dựng theo một chuẩn chung dựa trên các lỗi thường có đối với server Apache.

tác dụng:

- `HTTP Protection` - nhận diện những lỗ hổng của giao thức HTTP và khai báo những chính sách hữu dụng.
- `Real-time Blacklist Lookups` – sử dụng Party IP Reputation thứ 3.
- `Web-based Malware Detection`- nhận diện những trang web có nội dung độc hại bằng việc kiểm tra lại Google Safe Browsing API.
- `HTTP Denial of Service Protections`-Phòng chống tắc nghẽ trong giao thức HTTP và làm chậm tấn công DDOS
- `Common Web Attacks Protection`-nhận diện những tấn công an ninh vào những ứng dụng web nói chung.
- `Automation Detection`-nhận diện những máy tự động,thu thập thông tin, quét và những hoạt động bề ngoài độc hại.
- `Integration with AV Scanning for File Uploads`-nhận diễn những file độc hại được tải lên thông qua ứng dụng web.
- `Tracking Sensitive Data`- Theo dõi Credit Card hữu dụng và khóa những Credit Card bị lộ
- `Error Detection and Hiding` – che giấu những thông tin lỗi được gửi bởi server
- `Trojan Protection` –nhận diện những truy cập tới Trojan.

Ta cần phải dowload Core Rule tại địa chỉ sau:http://sourceforge.net/projects/mod-security/files/ModSecurity-crs/0-CURRENT/

#### Thiết lập chống một số lỗi cơ bản

- SQL Injection

Các từ khóa chính thường sử dụng trong tấn công SQL Injection và các regular expressions tương ứng:

```php!
UNION SELECT               union\s+select

UNION ALL SELECT           union\s+all\s+select

INTO OUTFILE               into\s+outfile

DROP TABLE                 drop\s+table

ALTER TABLE                alter\s+table

LOAD_FILE                 load_file

SELECT *                   select\s+*
```

‘\s’ được định nghĩa trong PCRE là một regular expression cho phép phát hiện mọi khoảng trắng và cả các mã thay thế (%20). Để chống lại tấn công SQL Injection, ta dựa vào các đặc điểm trên từ đó đưa ra rule sau:

```php!
SecRule ARGS "union\s+select" "t:lowercase,deny,msg:'SQL Injection'"

SecRule ARGS "union\s+all\s+select" "t:lowercase,deny,msg:'SQL Injection'"

SecRule ARGS "into\s+outfile" "t:lowercase,deny,msg:'SQL Injection'"

SecRule ARGS "drop\s+table" "t:lowercase,deny,msg:'SQL Injection'"

SecRule ARGS "alter\s+table" "t:lowercase,deny,msg:'SQL Injection'"

SecRule ARGS "load_file" "t:lowercase,deny,msg:'SQL Injection'"

SecRule ARGS "select\s+*" "t:lowercase,deny,msg:'SQL "
```

- XSS Attack

```php!
SecRule ARGS "alert\s+*\("t:lowercase,deny,msg:'XSS'"

SecRule ARGS "&\{.+\}" "t:lowchimercase,deny,msg:'XSS'"

SecRule ARGS "" "t:lowercase,deny,msg:'XSS'"

SecRule ARGS "javascript:"t:lowercase,deny,msg:'XSS'"

SecRule ARGS "vbscript:""t:lowercase,deny,msg:'XSS'"
```

- Website defacement
  Đây là kiểu tấn công dựa trên việc làm thay đổi nội dung web site theo ý muốn của hacker ví dụ:

```php!
SecRule REMOTE_ADDR ".*"  "phase:4,deny,chain,t:md5,t:hexEncode,

exec:/usr/bin/emailadmin.sh"

SecRule RESPONSE_BODY "!@contains %{MATCHED_VAR}"
```

- Directory indexing

```php!
# Prevent directory listings from accidentally being returned

SecRule REQUEST_URI "/$" "phase:4,deny,chain,log,msg:'Directory index returned'"

SecRule RESPONSE_BODY "Index of /"
```

- Chống DDos

```php!
SecAction initcol:ip=%{REMOTE_ADDR},nolog

SecRule REQUEST_LINE "^GET (?:/|.+\.html|.+\.php|.+\.cgi|.+\.pl) HTTP" " nolog,setvar:ip.ddos=+1,deprecatevar:ip.ddos=100/10"

SecRule IP:DDOS "@gt 35" "phase:1,id:'981052',t:none,log,drop,msg:'Client Connection Dropped due to high # of slow DoS alerts'"
```

### Logging

- Sử dụng SecDebugLog Dẫn hướng lựa chọn file để ghi lại các thông tin debug

```php!
SecDebugLog logs/modsec-debug.log
```

- Bạn có thể thay đổi mức độ chi tiết các thông tin được log thông qua Dẫn hướng

```php!
SecDebugLogLevel  4
```

Giá trị log có thể thay đổi từ 0-9:

- 0 – không ghi log.
- 1 –Chỉ liệt kê các request bị chặn.
- 2 –Cảnh báo.
- 3 – Thông báo cho admin
- 4 – Chi tiết về các transaction được xử lý.
- 5 – Cũng như số 4 như thêm những thông tin chi tiết hơn đã được xử lý
- 9 – Ghi lại mọi thứ, rất chi tiết và đầy đủ về toàn bộ thông tin.

### Audit logging

- ModSecurity hỗ trợ audit loging với đầy đủ thông tin và từ đó có thể lần ngược lại quá trình của kẻ tấn công, cũng như là chỉnh sửa các rules cho hợp lý tránh bị “false positive”:

```php!
SecAuditEngine On  //bật audit log lên
SecAuditLog logs/audit.log   //chỉ ra file lưu trữ log chính
SecAuditLog2 logs/audit2.log //chỉ ra file lưu trữ log phụ
```

SecAuditEngine chấp nhận 3 giá trị sau:

- On – log tất cả các requests
- Off – không log
- RelevantOnly – chỉ log những gì được sinh ra bởi các bộ lọc rules

## WAF - modsecurity trên nginx

- https://hackmd.io/@LsyWeJqxSYS5CYf0Hlbawg/SJUn8ixJi
- https://123host.vn/tailieu/kb/vps/huong-dan-cai-dat-modsecurity-len-nginx-tren-ubuntu-20-04.html
- https://www.youtube.com/watch?v=kBE0glft6LY
- https://www.youtube.com/watch?v=478ku0_2LvI

## Tham khảo

- https://viblo.asia/p/tich-hop-mod-security-cho-web-application-server-de-chong-lai-sql-injection-va-tan-cong-xss-bJzKmx6X59N
- https://whitehat.vn/threads/huong-dan-cai-dat-mod_security-cho-server-apache.34/
- https://thaibinh.gov.vn/attt/tin-tuc-su-kien/tuong-lua-ung-dung-web-modsecurity-va-cai-dat-de-bao-ve-webs.html
- https://www.youtube.com/watch?v=2rIRcI_bYgY
- https://www.youtube.com/watch?v=ZRor7xTgy04
