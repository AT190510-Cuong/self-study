# Các trường trong HTTP request, response

## HTTP

- HTTP là viết tắt của HyperText Transfer Protocol, là một giao thức truyền tải siêu văn bản, giúp cho các máy tính có thể giao tiếp với nhau qua mạng. HTTP là nền tảng của World Wide Web kết nối giữa máy chủ (server) và máy khách (client) trong cùng một hệ thống mạng. Điều này cho phép chúng ta truy cập vào các trang web, tải xuống các tệp tin, xem các hình ảnh, video… Ban đầu khi được thiết kế vào những năm 90, HTTP là một giao thức linh hoạt có khả năng mở rộng theo thời gian. Giao thức này hoạt động trên nền tảng TCP/IP và thường được truyền qua kết nối mã hóa TLS để bảo vệ dữ liệu.

![image](https://hackmd.io/_uploads/ryw71MCjp.png)

## HTTP request

![image](https://hackmd.io/_uploads/rJnVOl8sp.png)

![image](https://hackmd.io/_uploads/rJ9Q78Iop.png)

- Header thường được sử dụng để thực hiện các tác vụ như:
  - Chuyển hướng trang: Bằng cách sử dụng header, bạn có thể chuyển hướng người dùng đến một trang web khác hoặc trang mới sau khi xử lý một yêu cầu. Ví dụ: chuyển hướng sau khi người dùng đăng nhập thành công hoặc chuyển hướng từ một trang không tồn tại đến trang lỗi.
  - Đặt loại nội dung trả về: Header cho phép bạn định nghĩa kiểu dữ liệu nào được trả về cho trình duyệt. Ví dụ: đặt loại nội dung là HTML, JSON, XML, hoặc file ảnh.
  - Xử lý lỗi và mã trạng thái HTTP: Bằng cách sử dụng header, bạn có thể gửi mã trạng thái HTTP tương ứng với tình huống xử lý. Ví dụ: mã trạng thái 404 Not Found cho trang không tồn tại, mã trạng thái 500 Internal Server Error cho lỗi máy chủ.
  - Thiết lập các thông số và hạn chế của trang web: Header cũng cho phép bạn đặt các thông số và hạn chế của trang web như ngôn ngữ, mã hóa, cache control, cookie, v.v.

![image](https://hackmd.io/_uploads/SJpd1fSs6.png)

- Dòng đầu tiên của một request gồm 3 phần:

  - Phương thức đang được sử dụng, phổ biến nhất là GET. HTTP method (như GET, PUT, POST, HEAD, OPTIONS, …): miêu tả hành động sẽ được thực hiện
  - URL được request. Mục tiêu request, thường là URL, hoặc đường dẫn của giao thức, cổng, …
  - Phiên bản HTTP đang được sử dụng. Phiên bản HTTP: định nghĩa cấu trúc còn lại của message, cũng là phiên bản của reponse trả về

- **HTTP headers**: cấu trúc dạng key : value, có thể được chia thành nhiều nhóm:
  - **Request headers**: như User-Agent, Accept-Type, sửa request bằng việc chỉ định rõ hơn, đưa ra context (như Referer), ...
  - **General headers**: áp dụng cho cả message request và response, ko liên quan gì đến data được truyền trong body. Ví dụ: Connection: keep-alive: kiểm soát xem kết nối mạng có mở hay không sau khi giao dịch hiện tại kết thúc.
  - **Entity headers**: như Content-Length, áp dụng cho body của request

![image](https://hackmd.io/_uploads/BJDoQyIiT.png)

- Một số trường của header điển hình trong request: - **Referer**: cho biết URL mà từ đó request bắt nguồn
  ![image](https://hackmd.io/_uploads/HkNBKVAia.png)

Trong giao thức HTTP, Origin và Referer là hai trường tiêu đề (header) mà trình duyệt web gửi đi khi yêu cầu tới một trang web. Dù cả hai đều chứa thông tin về nguồn gốc của yêu cầu, chúng có mục đích và sử dụng khác nhau:

Referer: Đây là một trường tiêu đề HTTP chứa URL của trang mà người dùng đang đến từ. Nó được gửi đi bởi trình duyệt web khi một người dùng nhấp vào một liên kết hoặc thực hiện một yêu cầu HTTP khác từ một trang web khác. Trong nhiều trường hợp, trường tiêu đề này cung cấp cho máy chủ một phần thông tin về nguồn gốc của yêu cầu, giúp họ hiểu được ngữ cảnh của yêu cầu.

Origin: Trường tiêu đề Origin chỉ ra nguồn gốc của một tài nguyên HTTP. Nó cung cấp thông tin về nguồn gốc của tài nguyên được yêu cầu, bao gồm giao thức, tên miền và cổng. Thường thì trường tiêu đề này được sử dụng trong CORS (Cross-Origin Resource Sharing) để xác định xem một trang web có được phép truy cập vào tài nguyên từ một nguồn gốc khác hay không.

Tóm lại, Referer cho biết trang web mà yêu cầu đến từ, trong khi Origin cung cấp thông tin về nguồn gốc của tài nguyên được yêu cầu. Mặc dù cả hai đều liên quan đến nguồn gốc của yêu cầu, nhưng chúng được sử dụng trong các ngữ cảnh khác nhau và có mục đích sử dụng khác nhau trong giao thức HTTP. - **User-Agent**: thông tin về trình duyệt được sử dụng để tạo request
![image](https://hackmd.io/_uploads/B1ukt4Cop.png) - **Cookie**: gửi các thông số bổ sung mà server cấp cho client trước đó - **Host header**: xác định duy nhất của tên host, nó rất cần thiết khi nhiều trang web được host trên cùng một server. - **Accept**: loại nội dung có thể nhận được từ thông điệp response. Ví dụ: text/plain, text/html… - **Accept-Encoding**: các kiểu nén được chấp nhận. Ví dụ: gzip, deflate, xz, exi…

![image](https://hackmd.io/_uploads/rJFjY40s6.png)

![image](https://hackmd.io/_uploads/r15AYVAsp.png)

![image](https://hackmd.io/_uploads/S1fyKzAip.png)

Virtual Host là kỹ thuật cấu hình Web Server để
sử dụng nhiều tên miền trên một máy chủ, đồng
thời chia sẻ tài nguyên như RAM, CPU,..

- **Body**: không phải request nào cũng có body, request lấy dữ liệu về như GET, HEAD, DELETE, OPTIONS thường không có. Request gửi data tới server để update nó như POST thì có
- Body được chia làm 2 loại:

1. **Body với một resource (đơn lẻ):**
   - Loại này chỉ chứa một tài nguyên duy nhất, thường là một file hoặc một phần của nội dung. Được định nghĩa bởi hai headers chính: Content-Type để xác định loại nội dung và Content-Length để xác định kích thước của nội dung
   - Ví dụ: một yêu cầu POST có thể gửi một file ảnh duy nhất hoặc một đoạn văn bản duy nhất.
2. **Multiple-resource bodies (đa tài nguyên):**
   - Loại này thường sử dụng một multipart body, trong đó mỗi phần (part) của body có thể chứa một tài nguyên riêng biệt.
   - Mỗi phần trong body multipart có thể có các headers riêng để xác định loại nội dung, định dạng, v.v.
   - Đây thường được sử dụng khi cần gửi nhiều tài nguyên khác nhau trong một yêu cầu hoặc phản hồi.
   - Ví dụ: một yêu cầu POST có thể gửi nhiều hình ảnh hoặc nhiều tập tin khác nhau trong cùng một yêu cầu.
     ![image](https://hackmd.io/_uploads/SyXIs1Iip.png)

## HTTP Response

![image](https://hackmd.io/_uploads/SkBQKeUip.png)

- Dòng đầu tiên của một response gồm 3 phần:

  - Phiên bản HTTP đang được sử dụng
  - Status code: cho biết mã số thể hiện trạng thái kết quả request
  - Diễn giải status code bằng text

- Headers: cấu trúc dạng key : value gồm có 3 nhóm:
  - **Response headers**: bổ thêm thông tin về server
  - **General headers**: áp dụng cho cả message
  - **Entity headers**: áp dụng tới body của reponse, như Content-Length

![image](https://hackmd.io/_uploads/SyuroLUjp.png)

![image](https://hackmd.io/_uploads/B1T9nJLsT.png)

- Một số trường của header điển hình trong response: - **Server**: thông tin về phần mềm máy chủ đang được sử dụng, đôi khi là mô-đun đã cài đặt hay hệ điều hành máy chủ.
  ![image](https://hackmd.io/_uploads/Sybus4Aop.png) - **Set-Cookie**: cung cấp cho trình duyệt một cookie khác, lưu vào header Cookie của request tiếp theo. Thường sau khi đăng nhập sẽ được cấp trường này
  ![image](https://hackmd.io/_uploads/SJb4hNRj6.png) - **Content-Type**: chuẩn chung của một HTTP response có bao gồm message body, header này cho biết loại nội dung thực tế trong message body. VD: HTML, gif, png, mp4… - **Content-Length**: cho biết kích thước của message body tính bằng byte. - **Pragma**: chỉ dẫn trình duyệt không lưu response trong bộ nhớ đệm. - **Expires**: cho biết nội dung response đã hết hạn, do đó không nên được lưu trữ. - Set-Cookie header: lưu các tham số vào cookie của trình duyệt

![image](https://hackmd.io/_uploads/SJ8Yh4Ci6.png)

- **Body**:là nơi đóng gói dữ liệu để trả về cho client, thông thường trong duyệt web thì dữ liệu trả về sẽ ở dưới dạng một trang HTML để trình duyệt có thể thông dịch được và hiển thị ra cho người dùng. Không phải response nào cũng có, response với status code 201, 204 thường không có, gồm có 3 loại:
  - Body 1 resource (kích thước biết trước): Loại này bao gồm một tài nguyên duy nhất, thường là một file. Kích thước của tài nguyên được biết trước, do đó kích thước body cũng được xác định trước bởi header Content-Length.
  - Body 1 resource (kích thước không biết trước): Thay vì sử dụng Content-Length, loại này sử dụng mã hóa chunked bởi Transfer-Encoding.
  - Multiple-resource bodies (đa tài nguyên): Loại này sử dụng một multipart body, trong đó mỗi phần (part) của body có thể chứa một tài nguyên riêng biệt.

## Http request và response có chung cấu trúc như sau:

- **start-line**: miêu tả request để thực hiện (GET, POST, PUT, …), trạng thái thành công hay thất bại (qua các mã code)
- **HTTP headers**: có thể có hoặc không, chứa các thông tin của request (host, content-length, encoding, …) hoặc miêu tả phần body của message
- **Dòng kẻ trống**: là phần phần tách giữa header vs body
- **body**: Phần thân tùy chọn chứa dữ liệu được liên kết với request (như nội dung của biểu mẫu HTML) hoặc tài liệu được liên kết với reponse.

Phần body được tính sau dòng kẻ trống và kích thước của nó được chỉ định bởi các HTTP headers.
**start-line** + **HTTP headers** = **head của request**

![image](https://hackmd.io/_uploads/HylUZkLs6.png)

- ![image](https://hackmd.io/_uploads/BJWc9NAja.png)

- Trong HTTP, trường "Content-Type" trong tiêu đề (header) được sử dụng để xác định loại dữ liệu của nội dung được gửi trong yêu cầu hoặc phản hồi. Dưới đây là một số giá trị phổ biến của trường "Content-Type":
  - text/plain: Được sử dụng cho các tài liệu văn bản không được mã hóa đặc biệt.
  - text/html: Được sử dụng cho các tài liệu HTML.
  - application/json: Được sử dụng cho dữ liệu JSON.
  - application/xml: Được sử dụng cho dữ liệu XML.
  - application/x-www-form-urlencoded: Được sử dụng cho dữ liệu được mã hóa URL trong yêu cầu gửi từ một biểu mẫu HTML thông qua phương thức POST.
  - multipart/form-data: Được sử dụng cho dữ liệu biểu mẫu lớn hoặc không cấu trúc được gửi dưới dạng nhiều phần trong yêu cầu POST.
  - image/jpeg: Được sử dụng cho ảnh JPEG.
  - image/png: Được sử dụng cho ảnh PNG.
  - video/mp4: Được sử dụng cho video MP4.
  - audio/mpeg: Được sử dụng cho file âm thanh MPEG.
  - application/octet-stream: Được sử dụng cho các dữ liệu không xác định hoặc không thuộc các loại trên.
- Content Type cũng có thể được sử dụng để xác định ngôn ngữ và bộ mã hóa của nội dung. Ví dụ, Content Type \"text/html; charset=utf-8\" chỉ ra rằng nội dung là mã HTML với bộ mã hóa UTF-8.

- MIME type (Multipurpose Internet Mail Extensions) là một tiêu chuẩn Internet về định dạng cho thư điện tử.
  - Cấu trúc: type/subtype
  - Type: tổng quan về loại data, ví dụ như video, text
  - Subtype: chi tiết hơn cho Type.
- Type
  - Discrete(rời rạc): đại diện cho 1 tệp hoặc phương tiện, chẳng hạn như 1 tệp văn bản, nhạc hoặc video.
  - application: bất kì loại dữ liệu nhị phân nào không rơi vào các loại khác, dữ liệu sẽ được thực thi theo cách nào đó hoặc cần một ứng dụng hoặc danh mục ứng dụng cụ thể để sử. Ví dụ: application/pdf, application/pkcs8, and application/zip.
  - audio: audio hoặc dữ liệu nhạc, bao gồm audio/mpeg, audio/vorbis
  - example: chỉ là để ví dụ, ko nên dùng trong thực tế
  - image: ảnh hoặc dữ liệu đồ họa, gồm bitmap, vector, ảnh GIF, ... Ví dụ như image/jpeg, image/png, image/svg+xml
  - model: mẫu dữ liệu cho 3D object hoặc scene. Ví dụ model/3mf, model/vml
  - video: video data hoặc file, ví dụ như MP4 movies(video/mp4)
  - Multipart: một tài liệu bao gồm nhiều thành phần, mỗi phần có một lại MIME riêng, hoặc 1 loại nhiều phần có thể gói gọn nhiều tệp cùng nhau trong 1 giao dịch. Được gọi là tài liệu tổng hợp

## Các phương thức encode hay dùng

- Có 3 phương thức encode hay dùng
- **application/x-www-form-urlencoded** (the default): khi không muốn gửi file, url đã được mã hóa

## HTTP Methods

HTTP Là giao thức truyền siêu văn bản, nằm trong tầng Application - tầng cao nhất của bộ giao thức TCP/IP. Được sử dụng để truyền nội dung giữa Web Server đến Web Client. Cơ chế hoạt động request - response: Client sẽ gửi request đến Server, sau đó Server sẽ xử lý gì đó và trả về response cho Client. Đặc điểm: là 1 giao thức giao tiếp phi trạngthái ( stateless protocol) - mỗi request được xem là 1 phiên làm việc hoàn toàn độc lập - không lưu bất kỳ thông tin nào liên quan đến các lần request trước đó. Các method thông dụng của HTTP:

- **GET**: sử dụng để lấy thông tin từ server, request sử dụng GET chỉ nhận dữ liệu, không làm thay đổi dữ liệu
  - GET có thể được lưu trữ lại trong lịch sử trình duyệt
  - GET có thể được đánh dấu
  - GET giới hạn độ dài
  - GET có thể dùng để đầy dữ liệu lên . GET thì không có body nên khi gửi thì tất cả các parameter sẽ bị hiển thị lên url của request, xét về bảo mật thì đây sẽ không tốt. Post nó giấu paremeter trong Body và mã hóa chúng, sẽ an toàn hơn
- **HEAD**: tương tự GET nhưng không trả về phần body trong response mà truyền tải dòng trạng thái và phần header.
  - Nói một cách khác, nếu sử dụng phương thức GET tới đường dẫn /Books thì sẽ trả về danh sách các sản phẩm, còn khi sử dụng HEAD tới đường dẫn /Books nhưng không nhận được danh sách các sản phẩm.
  - Truy vấn HEAD hữu ích khi chúng ta sử dụng nó để kiểm tra API có hoạt động không do không có response body nên thời gian phản hồi nhanh hơn so với phương thức Get. Và thường được sử dụng để kiếm tra trước khi download file do cứ gọi đến api dowload sẽ download file nên thêm phương thức head vào nó kiểm tra xem api có đang hoạt động tốt không tránh down nhiều.
- **POST**: được sử dụng để gửi dữ liệu lên server để tạo tài nguyên
  - POST không được lưu trữ
  - POST không được lưu lại trong lịch sử trình duyệt
  - POST không giới hạn độ dài
- **PUT**: được dùng để gửi dữ liệu lên server để cập nhật tài nguyên, sẽ làm thay đổi thông tin nếu tài nguyên đã tồn tại
- **PATCH**: ghi đè các thông tin được thay đổi của đối tượng, cập một 1 phần của resource
- **DELETE**: xoá tài nguyên được chỉ định
- **CONNECT**: thiết lập một tunnel từ client tới server, thông qua proxy
- **OPTIONS**: cho biết methods khả dụng cho tài nguyên cụ thể
  ![image](https://hackmd.io/_uploads/S1ZqwfCoT.png)
  chúng ta có thể dùng lệnh `curl -X OPTIONS www.google.com -i` trên terminal để kiểm tra các HTTP method được dùng trên trang google.com
  ![image](https://hackmd.io/_uploads/B1fNOfAip.png)

- **TRACE**: thực hiện lặp lại thông báo kiểm tra cho tài nguyên đích, hữu ích cho việc gỡ lỗi

## Status Code

- 5 nhóm status code:
  - 1xx: request đã được nhận
    - 100 (continue): server đã nhận được một phần request, client nên tiếp tục gửi request
    - 101 (switching protocols): phản hồi header Upgrade từ client, chấp nhận yêu cầu chuyển đổi giao thức
    - 102 (processing): cho biết máy chủ đã nhận và đang xử lý yêu cầu nhưng chưa có phản hồi
    - 103 (early hint): cho phép người dùng tải trước tài nguyên trong khi máy chủ chuẩn bị phản hồi
  - 2xx: xử lý request thành công
    - 200 (OK): request thành công, kết quả phụ thuộc vào method
    - 201 (created): request thành công, kết quả là một tài nguyên mới được tạo ra. Đây thường là response của request POST hoặc PUT
    - 204 (no content): máy chủ xử lý yêu cầu thành công nhưng không có nội dung nào được trả lại
    - 206 (partial content): phản hồi header Range, xử lý thành công một phần request
  - 3xx: điều hướng lại
    - 301 (moved permanently): trang web được yêu cầu đã di chuyển vĩnh viễn tới URL mới
    - 302 (found): trang web được yêu cầu di chuyển tạm thời tới một URL mới
    - 304 (not modified): trang yêu cầu không được sửa đổi từ request cuối cùng, client có thể tiếp tuc sử dụng response được lưu trong catch
  - 4xx: lỗi ở phía client
    - 400 (bad request): máy chủ không hiểu request do lỗi của client
    - 401 (unauthorized): yêu cầu xác thực từ client, thường xuất hiện nếu client gửi request một trang đăng nhập
    - 403 (forbidden): máy chủ từ chối yêu cầu do client không có quyền truy cập vào nội dung đã yêu cầu, thường trả về nếu đăng nhập không thành công
    - 404 (not found): không thể tìm thấy trang yêu cầu
    - 405 (method not allowed): phương thức trong request không được hỗ trợ
    - 408 (request timeout): request tốn thời gian hơn response
    - 411 (length required): content-length không được xác định rõ
    - 413 (payload too large): máy chủ không thể xử lý do yêu cầu quá lớn
    - 414 (URI too long): URI do client yêu cầu dài hơn độ dài máy chủ có thể diễn giải
  - 5xx: lỗi ở phía server
    - 500 (internal server error): máy chủ gặp lỗi, không thể thực hiện request
    - 501 (no implemented): máy chủ không có chức năng thực hiện yêu cầu
    - 503 (service unavailable): máy chủ hiện không có sẵn (do quá tải hoặc bảo trì), đây là trạng thái tạm thời

## HTTP Headers

- Có thể chia header thành 4 kiểu:
  - General Header: áp dụng cho cả request và response
    - Connection: cho biết có nên đóng kết nối TCP sau khi quá trình truyền HTTP hoàn tất hay vẫn mở cho các message tiếp theo
    - Content-Encoding: chỉ ra loại mã hoá đang được sử dụng cho nội dung message
    - Content-Length: chỉ ra độ dài message tính bằng byte
    - Content-Type: huẩn chung của một HTTP response có bao gồm message body, header này cho biết loại nội dung thực tế trong message body. VD: HTML, gif, png, mp4…
    - Transfer-Encoding: chỉ định hình thức mã hoá để truyền tải nội dung một cách an toàn tới người dùng
  - Request header: chứa thông tin của request
    - Accept: cho server biết những loại nội dung nào được client chấp nhận. VD: image type, office document fomat…
    - Accept-Encoding: cho server biết loại mã hoá được client chấp nhận
    - Authorization: gửi đến server thông tin xác thực
    - Cookie: gửi cookie đến server
    - Host: cho biết tên host (được xác định duy nhất), cần thiết khi nhiều trang web được lưu trữ trên cùng một server
    - If-Modified-Since: chỉ định thời điểm trình duyệt nhận request lần cuối. Nếu tài nguyên không thay đổi kể từ thời điểm đó, server hướng dẫn client sử dụng bản sao lưu trong bộ nhớ đệm bằng response có status code là 304
    - • If-None-Match*:* yêu cầu server trình bày method được yêu cầu chỉ khi một trong số giá trị đã cho của thẻ này kết nối với các thẻ đối tượng đã được cung cấp biểu diễn bởi Etag.
    - Origin: chỉ ra nguồn gốc request
    - Referer: cho biết nguồn gốc, đường dẫn, chuỗi truy vấn… của request
    - User-Agent: thông tin về trình duyệt được sử dụng để tạo request
  - Response header: chứa thông tin của response
    - Access-Control-Allow-Origin: chỉ ra liệu tài nguyên có thể được truy xuất thông qua request Ajax Cross-domain
    - Catch-Control: chuyển các chỉ thị bộ nhớ đệm đến trình duyệt
    - Location: được sử dụng trong các response chuyển hướng (những response có mã trạng thái bắt đầu bằng 3) để chỉ định mục tiêu của chuyển hướng
    - Set-Cookie: cấp cookie cho trình duyệt mà nó sẽ được gửi lại server trong các request tiếp theo
    - X-Frame-Options: chỉ ra liệu response hiện tại có thể tải trong khung trình duyệt hay không và như thế nào
    - WWW-Authenticate: được sử dụng trong response có mã trạng thái là 401 để cung cấp chi tiết về các loại xác thực mà Server hỗ trợ

## Cookies

- Cookies là phần dữ liệu được server gửi tới trình duyệt vào lần đầu truy cập website hoặc không tìm thấy request của trình duyệt gửi lên. Sau đó cookies được lưu lại trên trình duyệt của client và được gửi lại server trong lần request tiếp theo.
- Cookie thường bao gồm một cặp name/value. Ngoài giá trị thực của cookie, Set-Cookie có thể bao gồm các thuộc tính tuỳ chọn:
  - **Expire**: đặt ngày cookie hết hiệu lực. Nếu thuộc tính này không được đặt, cookie chỉ được sử dụng trong phiên trình duyệt hiện tại
  - **Domain**: chỉ định miền mà cookie hợp lệ. Tên miền này phải giống hoặc là tên miền mà từ đó cookie được nhận
  - **Path**: được sử dụng để chỉ định đường dẫn URL mà cookie hợp lệ
  - **Secure**: nếu thuộc tính này được đặt, cookie sẽ chỉ được gửi trong HTTPS request
  - **HttpOnly**: nếu thuộc tính này được đặt, cookie không thể được truy cập trực tiếp qua JavaScript phía client mà chỉ được xử lí bởi server
- Tồn tại cho đến khi nó hết hạn Khi thực hiện một http request, thì browser sẽ dựa vào url, tìm kiếm các cookie tương ứng với domain của url vừa nhập để gửi hết cookie hiện tại lên server. Giới hạn lưu trữ: 4kb. Trong trường hợp cookie nhiều hơn 4kb thì những giá trị cookie cũ nhất sẽ bị xóa đi Set càng nhiều cookie thì request càng lớn -> giảm tốc độ

## Chu trình xử lý của trình duyệt từ khi xử lý đến khi render ra toàn bộ nội dung

![image](https://hackmd.io/_uploads/r117efAiT.png)

- HTTP sử dụng kết nối kiểm soát ở tầng truyền tải. Mặc dù không yêu cầu sự kết nối, HTTP phụ thuộc vào TCP, một giao thức đáng tin cậy, để thiết lập kết nối trước khi trao đổi thông tin giữa client và server. Trong HTTP/1.0, mỗi cặp yêu cầu - phản hồi mở một kết nối TCP mới, làm tăng độ trễ. HTTP/1.1 sử dụng pipelining và kết nối liên tục để giảm thiểu vấn đề này, trong khi HTTP/2 tổ chức thông điệp qua một kết nối, làm cho kết nối ổn định hơn. Đang có các thử nghiệm để phát triển giao thức truyền tải tốt hơn, như thử nghiệm của Google với QUIC trên UDP để cung cấp sự đáng tin cậy và hiệu quả.

![image](https://hackmd.io/_uploads/rJggGf0oa.png)

![image](https://hackmd.io/_uploads/BkW0bMRj6.png)

![image](https://hackmd.io/_uploads/rJfZMGCs6.png)

![image](https://hackmd.io/_uploads/rJmgLIIsa.png)

1. Người dùng nhập vào thành tìm kiếm của trình duyệt web một địa chỉ (domain name). VD: facebook.com
2. Trình duyệt gửi yêu cầu đến DNS. DNS phân giải domain name thành IP của web server chứa source code ứng với domain đó. Dễ hiểu hơn là DNS đã lưu lại IP của server từ lúc đăng ký domain, lúc cần thì sẽ đưa ra. (tham khảo thêm https://www.youtube.com/watch?v=FBF-xXX7nVM)
   ![image](https://hackmd.io/_uploads/S1t14aSsa.png)
3. Trình duyệt tiếp tục gửi yêu cầu tới web server thông qua IP đã nhận được.
4. Khi nhận được yêu cầu, web server sẽ xử lý thông tin và trả về nội dung website được yêu cầu (dưới dạng file bao gồm HTML/CSS, hình ảnh, video…)
5. Sau khi nhận được tài nguyên từ web server, trình duyệt sẽ render thành giao diện website chúng ta nhìn thấy.

## Cấu trúc URL

xem tại https://hackmd.io/@monstercuong7/HJ9mz75qT

## HTTP/2 Frames

- Với sự phát triển nhanh chóng của web, với nhiều thành phần hơn css, js... đồng nghĩa với việc chúng ta sẽ cần nhiều tài nguyên hơn và có trường hợp sẽ phải tải đồng thời nhiều tài nguyên. Điều mà khi thực hiện bằng cơ chế 1 connection / 1 tài nguyên của HTTP 1.0 sẽ không đạt được sự tối ưu về băng thông.
- Nén header và dữ liệu:
  - HTTP/2 cho phép nén cả header và dữ liệu trong mỗi khung, trong khi HTTP/1.x chỉ nén được dữ liệu.
  - Header thường bị lặp lại giữa các yêu cầu và phản hồi, vì vậy việc nén header giúp giảm băng thông cần thiết và cải thiện hiệu suất.
- Sử dụng khung (frames) và luồng (streams):
  - HTTP/2 chia mỗi tin nhắn HTTP thành các khung, bao gồm cả khung header và khung dữ liệu.
  - Các khung được gắn vào một luồng, cho phép nhiều luồng hoạt động đồng thời trên cùng một kết nối TCP.
  - Điều này giúp tăng tốc độ truyền tải bằng cách loại bỏ hiện tượng cản trở (blocking) trong việc gửi và nhận dữ liệu, so với việc sử dụng nhiều kết nối TCP song song trong HTTP/1.x.
- Dữ liệu truyền tải dạng nhị phân
  - HTTP/2 truyền dữ liệu ở dạng nhị phân thay vì dạng text như HTTP/1.x. Giao thức nhị phân hiệu quả hơn để phân tích cú pháp, gọn nhẹ hơn, và quan trọng nhất, chúng ít bị lỗi hơn nhiều so với các giao thức văn bản như HTTP/1.x. Bởi giao thức nhị phân không phải xử lý các trường hợp như khoảng trắng, viết hoa, kết thúc dòng, dòng trống...
- Phản hồi ưu tiên (prioritization)
  - Trong HTTP/1.1, server phải gửi phản hồi theo cùng trật tự nhận truy vấn. HTTP/2 thì giải quyết bất đồng bộ, nên các truy vấn nhỏ hơn hoặc nhanh hơn có thể được xử lý sớm hơn. Đồng thời, cho phép trình duyệt có thể sắp xếp thứ tự ưu tiên tải về cho các tài nguyên nào quan trọng dùng để hiển thị website.
- mục tiêu của HTTP/2 là cải thiện tốc độ tải trang, chúng ta sẽ cùng tìm hiểu một số đặc điểm giúp HTTP/2 đạt được mục tiêu này.
  HTTP/2 thêm tính năng: nó chia HTTP/1.x message thành các frame mà sẽ được gắn vào 1 luồng. Dữ liệu và header frame được tách ra, điều này giúp header nén được.

![image](https://hackmd.io/_uploads/rkakmeLoa.png)

Nhiều luồng có thể được kết hợp với nhau, giúp tạo ra ghép kênh, tối ưu sử dụng băng thông, tiết kiệm thời gian. Vì HTTP hoạt động ở tầng ứng dụng cần giao thức chuyền tải ở tầng dưới vận chuyển thông tin và nó truyền thông tin qua giao thức TCP:

- Với HTTP/1 thì mỗi 1 tài nguyên khác nhau trên 1 trang web sẽ cần 1 đường truyền TCP khác nhau, mà như các bạn biết TCP được thiết lập phải trải qua quá trình bắt tay 3 bước khiến trang web của chúng ta load lâu hơn

![image](https://hackmd.io/_uploads/H1xvBfCop.png)

- Trong khi đó HTTP/2 dùng 1 đường chuyền TCP trải qua 1 quá trình thiết lập bắt tay 3 bước của TCP nên sẽ tiết kiệm thời gian

![image](https://hackmd.io/_uploads/BJbbQz0oT.png)

![image](https://hackmd.io/_uploads/SJcxXxLja.png)

Để dễ hiểu hơn về vấn đề này, hãy tưởng tượng việc chúng ta vào website như vào 1 nhà hàng vậy. Và khi vào nhà hàng, ví dụ chúng ta sẽ gọi 10 món, hãy xem cách mà nhà hàng phục vụ chúng ta ở từng phiên bản:

- HTTP/1: Mỗi 1 người phục vụ sẽ chỉ nhận 1 order và mang lên đúng món đó, không nhận thêm bất cứ ordẻ nào nữa. Như vậy với 10 món, chúng ta sẽ phải gọi đến 10 ông phục vụ. Nhà hàng vừa tốn tiền thuê nhân công, mà mình thì tốn thời gian gọi mỏi mồm mới order đủ món, dỗi vl 🙄
- HTTP/1.1: Rút kinh nghiệm lần trước, nhà hàng training mấy ông phục vụ để nhận được nhiều order hơn, nhưng chỉ nhận 1 order 1 lần, mang món lên mới nhận order tiếp, chắc sợ quên 🙄. Để gọi đồ nhanh hơn bạn có thể gọi thêm 2-3 ông phục vụ nữa, tùy sức. Nhìn chung cách này khá là ổn, training nhân viên dễ, nên được dùng đến tận bây giờ, có mỗi cái là chưa tối ưu tối đa. Mấy ông này gọi là persistent connection. Vẫn là thời điểm này, nhà hàng có training 1 ông nhân viên đặc biệt. Ông này làm việc thông minh hơn 1 tí là ghi hết order vào luôn rồi bắt đầu mang đồ lên. Nhưng ông này làm việc hơi máy móc, phải trả đồ theo đúng thứ tự order mới chịu. Chẳng may gọi cơm, canh, cá mà hết mất cơm thì bắt ngồi chờ chứ nhất quyết ko cho ăn cá, dỗi vl 🙄 Thêm vào đấy, training mấy ông này khó hơn mấy ông bình thường nên đến 2018 thì mấy ông này không được dùng nữa. Mấy ông này được gọi là pipelining connection.

<img src="https://images.viblo.asia/726ca216-d7a3-4c9e-9853-5bbe4bc25f11.gif">

- HTTP/2: Nhà hàng học được công nghệ training mới, mấy ông nhân viên vẫn ghi hết order vào luôn rồi bắt đầu mang đồ lên. Nhưng mấy ông này sẽ linh hoạt hơn, món nào có trước mang lên trước, thâm chí món nào to quá thì mang từng phần xen kẽ cũng làm đc. Do đó, giảm được rất nhiều thời gian chờ, chỉ cần 1 người cũng phục vụ được 1 bàn, giảm thêm được cả chi phí thuê nhân viên luôn.

<img src="https://images.viblo.asia/54f0919a-4c83-4cf3-8b11-0ae343942e91.gif">

## Đọc thêm

- https://xaydungso.vn/blog/giai-thich-content-type-la-gi-va-cach-su-dung-trong-web-design-vi-cb.html
- https://viblo.asia/p/bao-mat-ung-dung-web-tong-quan-ve-http-RQqKLAqpZ7z
- https://websitehcm.com/header-trong-php-la-gi/
