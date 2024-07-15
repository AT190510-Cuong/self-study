# 1. Linux

## Cấu trúc thư mục Linux

![image](https://hackmd.io/_uploads/rkuRsagOC.png)

### File hệ thống Ext2, Ext3 & Ext4 trong Linux

- Trong hệ thống Linux, tất cả đều được cấu hình và coi như là file. Không chỉ bao gồm file text, ảnh, các chương trình biên dịch mà còn cả các thư mục, phân vùng và drive thiết bị phần cứng đều được hệ thống nhìn nhận như một file.

- Các hệ thống tệp Ext2, Ext3 và Ext4 là những hệ thống tệp phổ biến được sử dụng trong các hệ điều hành Linux. Dưới đây là mô tả chi tiết về từng hệ thống tệp này:

| Tính năng                          | Ext2         | Ext3         | Ext4           |
| ---------------------------------- | ------------ | ------------ | -------------- |
| **Giới thiệu**                     | 1993         | 2001         | 2008           |
| **Journaling**                     | Không        | Có           | Có             |
| **Kích thước hệ thống tệp tối đa** | 4 TB         | 32 TB        | 1 EB           |
| **Kích thước tệp tối đa**          | 2 TB         | 2 TB         | 16 TB          |
| **Cấp phát inode**                 | Tĩnh         | Tĩnh         | Động           |
| **Lưu trữ dựa trên extent**        | Không        | Không        | Có             |
| **Tương thích ngược**              | N/A          | Ext2         | Ext3, Ext2     |
| **Tương thích tiến**               | Ext3, Ext4   | Ext4         | N/A            |
| **Chống phân mảnh trực tuyến**     | Không        | Không        | Có             |
| **Cấp phát trễ**                   | Không        | Không        | Có             |
| **Cấp phát khối đa**               | Không        | Không        | Có             |
| **Kiểm tra fsck nhanh**            | Không        | Không        | Có             |
| **Xử lý dấu thời gian cải tiến**   | Không        | Không        | Có             |
| **Kiểm tra tổng của nhật ký**      | Không        | Không        | Có             |
| **Tùy chọn gắn kết mặc định**      | Data=ordered | Data=ordered | Data=writeback |
| **Rào cản mặc định**               | Không        | Có           | Có             |

- Nhìn chung, Ext4 là phiên bản tiên tiến nhất trong ba hệ thống tệp này, cung cấp nhiều tính năng và cải tiến hiệu suất, đồng thời vẫn duy trì sự tương thích với các phiên bản trước đó.

### các thư mục trong Linux và chức năng

- Linux quản lý hệ thống trên một "hệ thống tệp tin" duy nhất, bắt đầu ở gốc là thư mục root (/) đây là thư mục ở cấp cao nhất. Cấu trúc cơ bản của hệ thống Linux như sau:

![image](https://hackmd.io/_uploads/Hyi_sax_A.png)

- `/bin`: User binaries - thư mục lưu trữ các file nhị phân chương trình thực thi của người dùng như: pwd, cat, cp, ...

- `/sbin`: Chứa đựng các file thực thi dạng nhị phân của các chương trình cơ bản giúp hệ thống hoạt động. Các chương trình trong /sbin thường được sử dụng cho mục đích là duy trì và quản trị hệ thống => dành cho người dùng admin quản trị hệ thống - người dùng root hoặc superuser.Một số chương trình trong thư mục này như: init, iptables, fdisk, ...

- `/boot`: boot loader file - Chứa các tệp tin khởi động và cả nhân kernel là vmlinuz

- `/dev`: Các file thiết bị - nơi lưu trữ các phân vùng ổ cứng, thiết bị ngoại vi như usb, ổ đĩa cắm ngoài hay bất cứ thiết bị nào được gán vào hệ thống.

- `/etc`: Chứa file cấu hình cho các chương trình hoạt động. Chúng thường là các tệp tin dạng text thường. Chức năng gần giống "Control panel" trong Windows. Các cấu hình trong /etc thường ảnh hưởng tới tất cả người dùng trong hệ thống.Trong /etc còn chứa các shell scripts dùng để khởi động hoặc tắt các chương trình khác. Ví dụ: /etc/resolve.conf, sysctl.conf, ...

- `/home`: thư mục chứa các file cá nhân của từng user.
- `/lib`: Chứa các file library hỗ trợ cho các file thực binary. Mỗi khi cài đặt phần mềm trên Linux, các thư viện cũng tự động được download, và chúng hầu hết được bắt đầu với lib\*.. Đây là các thư viện cơ bản mà Linux cần đề làm việc. Không giống như trong Windows, các thư viện có thể chia sẻ và dùng chung cho các chương trình khác nhau. Đó là một lợi ích trong hệ thống tệp tin của Linux.
- `/media`: Chứa thư mục dùng để mount cho các thiết bị có thể gỡ bỏ, di chuyển khỏi hệ thống được như CDROM, floppy, ...

- `/mnt`: Chứa các thư mục dùng để system admin thực hiện quá trình mount. Như đã nói, hệ điều hành Linux coi tất cả là các file và lưu giữ trên một cây chung. Đây chính nơi tạo ra các thư mục để 'gắn' các phân vùng ổ đĩa cứng cũng như các thiết bị khác vào. Sau khi được mount vào đây, các thiết bị hay ổ cứng được truy cập từ đây như là một thư mục. Trong một số hệ điều hành, các ổ đĩa chưa được gắn sẵn vào hệ thống bởi fstab sẽ được gắn ở đây.
- `/opt`: Tên thư mục này nghĩa là optional (tùy chọn), nó chứa các ứng dụng thêm vào từ các nhà cung cấp độc lập khác. Các ứng dụng này có thể được cài ở /opt hoặc một thư mục con của /opt
- `/proc`: Chứa đựng thông tin về quá trình xử lý của hệ thống.
- /root: Thư mục home của người dùng root.
- /usr: Chứa các file binary, library, tài liệu, source-code cho các chương trình.

  - `/usr/bin` chứa file binary cho các chương trình của user. Nếu như một user trong quá trình thực thi một lệnh ban đầu sẽ tìm kiếm trong /bin, nếu như không có thì sẽ tiếp tục nhìn vào /usr/bin. Ví dụ một số lệnh như at. awk, cc...
  - `/usr/sbin` chứa các file binary cho system administrator. Nếu như ta không tìm thấy các file system binary bên dưới /sbin thì ta có thể tìm ở trong /usr/sbin. Ví dụ một số lệnh như cron, sshd, useradd, userdel
  - `/usr/lib` chứa các file libraries cho /usr/bin và /usr/sbin
  - `/usr/local` dùng để chứa chương trình của các user, các chương trình này được cài đặt từ source. Ví dụ khi ta install apache từ source thì nó sẽ nằm ở vị trí là /usr/local/apache2

- `/var`: Chứa đựng các file có sự thay đổi trong quá trình hoạt động của hệ điều hành cũng như các ứng dụng
  - Nhật ký của hệ thống `/var/log`
  - database file `/var/lib`
  - email `/var/mail`
  - Các hàng đợi in ấn: `/var/spool`
  - lock file: `/var/lock`
  - Các file tạm thời cần cho quá trình reboot: `/var/tmp`
  - Dữ liệu cho trang web: `/var/www`

| Window       | Linux    | mean                                                                     |
| ------------ | -------- | ------------------------------------------------------------------------ |
| Program File | /usr/bin | chứa tệp thực thi ứng dụng được cài đặt trên hệ thống                    |
| Window       | /etc     | chứa tệp tin cấu hình và các thành phần hệ thống quan trọng              |
| users        | home     | chứa thư mục cá nhân của người dùng gồm tệp tin cá nhân và thư mục riêng |
| Program Data | /var     | chứa dữ liệu chung cho các ứng dụng được cài đặt trên hệ thống           |
| Temp         | tmp      | lưu trữ tệp tin tạm thời                                                 |

### cài đặt ứng dụng theo 3 cách

1. Cài đặt phần mềm bằng apt
   - apt là công cụ quản lý gói chính trên Ubuntu. Bạn có thể cài đặt phần mềm từ kho lưu trữ chính thức của Ubuntu.
2. Cài đặt phần mềm từ tệp .deb
   - Bạn có thể tải xuống các tệp .deb từ trang web của nhà phát triển và cài đặt chúng bằng dpkg.
   - `sudo dpkg -i [tên_tệp].deb`
3. Cài đặt phần mềm bằng snap
   - `sudo snap install [tên_phần_mềm]`

## tìm kiếm tài nguyên với find

![image](https://hackmd.io/_uploads/H17D5ClO0.png)

1. Tìm kiếm theo tên tệp

- `find [đường_dẫn_bắt_đầu] -name [tên_tệp]`

- VD: `find . -name "example.txt"`

2. Tìm kiếm theo loại tệp

- `find [đường_dẫn_bắt_đầu] -type [loại_tệp]`
- Ví dụ:
  - Tìm tất cả các thư mục bắt đầu từ thư mục hiện tại:`find . -type d`
  - Tìm tất cả các tệp thông thường (regular files) bắt đầu từ thư mục hiện tại:`find . -type f`

3. Tìm kiếm theo kích thước tệp
   - `find [đường_dẫn_bắt_đầu] -size [kích_thước]`
4. Tìm kiếm theo thời gian chỉnh sửa
   - `find [đường_dẫn_bắt_đầu] -mtime [số_ngày]`
   - Ví dụ:
     - Tìm tất cả các tệp được chỉnh sửa trong vòng 7 ngày qua bắt đầu từ thư mục hiện tại:`find . -mtime -7`
     - Tìm tất cả các tệp được chỉnh sửa hơn 30 ngày trước bắt đầu từ thư mục hiện tại:`find . -mtime +30`
5. Kết hợp nhiều tiêu chí tìm kiếm - `find [đường_dẫn_bắt_đầu] [tiêu_chí_1] [tiêu_chí_2] ...` - Ví dụ:
   Tìm tất cả các tệp có phần mở rộng .txt và có kích thước lớn hơn 1 MB bắt đầu từ thư mục hiện tại:`find . -name "*.txt" -size +1M`
6. Thực hiện hành động trên các tệp được tìm thấy
   - `find [đường_dẫn_bắt_đầu] [tiêu_chí] -exec [lệnh] {} \;`
   - Tìm tất cả các tệp có phần mở rộng .log và hiển thị chi tiết về chúng:`find . -name "*.log" -exec ls -lh {} \;`

- `{}`: Thay thế cho tên tệp hoặc thư mục được tìm thấy bởi find. Mỗi tệp hoặc thư mục được tìm thấy sẽ thay thế {}
- `\;`: Kết thúc lệnh -exec. Dấu chấm phẩy (;) được thoát bởi dấu gạch chéo ngược (\) để ngăn không cho shell của bạn hiểu nhầm đó là dấu chấm phẩy kết thúc dòng lệnh.

## lập lịch Sử Dụng Crontab

![image](https://hackmd.io/_uploads/SypDVL-_R.png)

- https://viblo.asia/p/lap-lich-tasks-tren-linux-su-dung-crontab-6J3Zg28MKmB

- Crontab (CRON TABLE) là một tiện ích cho phép thực hiện các tác vụ một cách tự động theo định kỳ, ở chế độ nền của hệ thống. Crontab là một file chứa đựng bảng biểu (schedule) của các entries được chạy.
- Crontab (cron xuất phát từ "chronos", theo tiếng Hy Lạp có nghĩ là thời gian, tab là viết tắt của table), được tạo ra trên Unix và hoặc những hệ điều hành nhân Unix, thường dùng để lập lịch cho các câu lệnh để thực thi định kỳ
- Để xem được những crontab nào đang chạy trên hệ thống của bạn, bạn có thể mở terminal và chạy: `sudo crontab -l`
- Để chỉnh sửa danh sách các crontab này, bạn có thể chạy: `sudo crontab -e`

- chọn trình soạn thảo để edit crontab
  ![image](https://hackmd.io/_uploads/HkzmuIbuC.png)

![image](https://hackmd.io/_uploads/H1p3u8WdC.png)

- VD: `* * * * * /bin/execute/this/script.sh`

```
*     *     *     *     *     command to be executed
-     -     -     -     -
|     |     |     |     |
|     |     |     |     +----- day of week (0 - 6) (Sunday=0)
|     |     |     +------- month (1 - 12)
|     |     +--------- day of month (1 - 31)
|     +----------- hour (0 - 23)
+------------- min (0 - 59)

```

- Như bạn đã nhìn thấy, có 5 dấu sao. Những dấu sao này thể hiện những thành phần khác nhau của ngày theo thứ tự sau:
  - minute - phút (0 - 59)
  - hour - giờ (0 - 23)
  - day or month - ngày trong tháng (0 - 31)
  - month - tháng (1 - 12)
  - day of week (0 - 6 ~ Sunday - Saturday)
- Nếu bạn để toàn dấu sao, nó có nghĩa là "mỗi".
- VD Thực thi vào 1AM từ Thứ Hai đến Thứ Sáu

  - `0 1 * * 1-5 /bin/execute/this/script.sh`
    - minute - phút: 0
    - of hour - của giờ: 1
    - of day of month - Của ngày trong tháng: (every day of month)
    - of month - Của tháng: \* (every month)
    - and weekdays - Và ngày trong tuần: 1-5 (=Monday-Friday)

- Từ khóa đặc biệt

```
@reboot         Chạy một lần mỗi khi khởi động lại
@yearly          Chạy một lần mỗi năm    "0 0 1 1 *"
@annually     (Tương tự @yearly)
@monthly     Chạy  mỗi tháng một lần  "0 0 1 * *"
@weekly       Chạy mỗi tuần một lần  "0 0 * * 0"
@daily           Chạy một lần mỗi ngày    "0 0 * * *"
@midnight   (Tương tự @daily)
@hourly        Chạy một lần mỗi giờ    "0 * * * *"
```

- VD `@daily /bin/execute/this/script.sh`

- Mọi users, cũng như admin của hệ thống Linux, sẽ thường xuyên cần thực hiện một số tác vụ tự động vào những thời điểm nào đó hàng ngày.

  - Ví dụ, một admin của hệ thống có thể cần giám sát việc sử dụng dung lượng ổ đĩa cứng, RAM,... của hệ thống. Trong những trường hợp này, một bộ lập lịch cron là một công cụ rất tiện dụng để đạt được mục đích này.

  - Giả sử rằng admin của hệ thống cần thực thi một script /usr/local/sbin/backup.sh vào lúc 2:36 AM mỗi ngày Chủ Nhật hàng tuần. Trong trường hợp này, admin cần chỉnh sửa file crontab của mình như trong hình bên dưới:

![image](https://hackmd.io/_uploads/S11uTIZO0.png)

Định dạng của một crontab khá đơn giản, chúng được chia thành 7 trường ngăn cách nhau bởi dấu space hoặc dấu tab:

- Trường đầu tiên mô tả phút (giá trị từ 0-59)
- Trường thứ 2 mô tả giờ (giá trị từ 0-23)
- Trường thứ 3 mô tả ngày của tháng (giá trị từ 1-31)
- Trường thứ 4 mô tả tháng (giá trị từ 1-12)
  Trường thứ 5 mô tả ngày trong tuần (giá trị từ 0-7)
- Trường thứ 6 mô tả chúng ta sẽ thực thi câu lệnh với quyền của account nào
- Trường thứ 7 mô tả câu lệnh chúng ta sẽ thực thi

Dưới đây là một số crontab cơ bản khác:

| Crontab        | Mô tả                                       |
| -------------- | ------------------------------------------- |
| _/5 _ \* \* \* | Chạy crontab job mỗi 5 phút một lần         |
| 0 \* \* \* \*  | Chạy crontab job mỗi một giờ một lần        |
| 0 0 \* \* \*   | Chạy crontab job vào lúc 00:00 giờ mọi ngày |

- Có rất nhiều services trong Linux sử dụng crontab tự động. Chúng lưu những cấu hình của bộ lập lịch Crontab trực tiếp trong thư mục `/etc/cron.d`.Bất cứ file nào được lưu trong thư mục này sẽ được tự động lấy ra và thực thi bởi bộ lập lịch Crontab.

- Các admin trong hệ thống linux có thể tận dụng được những thư mục cấu hình crontab có sẵn như `/etc/cron.daily, /etc/cron.hourly, /etc/cron.monthly and /etc/cron.weekly`

- Mỗi người dùng có một cron schedule riêng, file này thường nằm ở `/var/spool/cron`

![image](https://hackmd.io/_uploads/SJPCXDb_0.png)

```
crontab -e: tạo,  chỉnh sửa các crontab
crontab -l: Xem các Crontab đã tạo
crontab -r: xóa file crontab
```

- https://cloud.z.com/vn/news/crontab/

Có hai loại tệp crontab chính:

1. Crontab của người dùng cá nhân:
   - Tệp crontab cho mỗi người dùng được lưu trong thư mục /var/spool/cron/crontabs hoặc /var/spool/cron (tùy thuộc vào hệ điều hành).
   - Tên tệp thường là tên người dùng. Ví dụ, nếu tên người dùng là user1, tệp crontab của họ sẽ có đường dẫn là /var/spool/cron/crontabs/user1 hoặc /var/spool/cron/user1.
2. Crontab của hệ thống:
   - Hệ thống có một tệp crontab toàn cục thường được lưu tại /etc/crontab.
   - Ngoài ra, có thể có các tệp crontab riêng cho các dịch vụ hoặc ứng dụng trong thư mục /etc/cron.d/.

Crontab cá nhân của người dùng user1:

```
/var/spool/cron/crontabs/user1
```

Crontab hệ thống:

```
/etc/crontab
```

Crontab cho các tác vụ đặc biệt:

```
/etc/cron.d/
```

Nội dung của /etc/crontab
Tệp crontab của hệ thống /etc/crontab có định dạng hơi khác so với crontab của người dùng vì nó có thêm trường để chỉ định người dùng mà lệnh sẽ được chạy dưới quyền của họ. Ví dụ:

```
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
```

1. Crontab cá nhân của người dùng

`crontab -e`

- VD: `30 2 * * * /path/to/command`

2. Crontab của hệ thống

- Chỉnh sửa tệp /etc/crontab
  Bạn cần quyền root để chỉnh sửa tệp này. Sử dụng lệnh sudo để mở tệp với trình soạn thảo văn bản yêu thích của bạn. Ví dụ:
  `sudo nano /etc/crontab`
  Ví dụ
  Để chạy một lệnh vào 3:00 chiều mỗi Chủ nhật dưới quyền root, thêm dòng sau vào /etc/crontab:
  `0 15 * * 0 root /path/to/command`
- Chỉnh sửa tệp trong thư mục /etc/cron.d/
  Bạn cũng có thể thêm tệp crontab riêng lẻ vào thư mục này. Mỗi tệp phải có định dạng tương tự như /etc/crontab với trường người dùng.

Ví dụ
Tạo một tệp mới trong /etc/cron.d/:
`sudo nano /etc/cron.d/mycron`
`0 5 1,15 * * user /path/to/command`

![image](https://hackmd.io/_uploads/S1Rk-dZ_R.png)

![image](https://hackmd.io/_uploads/ryh0x_ZO0.png)

![image](https://hackmd.io/_uploads/SJvbDGM_0.png)
