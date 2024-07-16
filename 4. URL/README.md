# URL

- URL (Uniform Resource Locator - Định vị tài nguyên thống nhất) là một định danh duy nhất cho tài nguyên web mà qua đó có thể truy xuất đến nó.

Cấu trúc đầy đủ của một URL như sau:

![image](https://hackmd.io/_uploads/Bk6UG79cp.png)

1. **Scheme**: xác định giao thức được sử dụng để truy cập tài nguyên
2. **Indicator of a hierachical**: cố định
3. **Credentials to access to resource**: có thể chỉ ra username, thậm chí là password, phần này có thể có hoặc không
4. **Server address**: xác đinh địa chỉ của server
5. **Server port**: có thể có hoặc không, thường được thêm vào nếu nó khác với số cổng mặc định của giao thức
6. **Hierarchical file path**: ánh xạ để xác định vị trí tài nguyên sẽ được lấy về từ server
7. **Query string**: có thể có hoặc không, cung cấp thêm các thông tin truy vấn cho server
8. **Fragment ID**: có vai trò tương tự như query string nhưng cung cấp các tuỳ chọn cho client, giá trị này không được gửi đến server

- **Lưu ý**: Các ký tự đặc biệt như :, `/`, `#`, `[`, `]`, `@` có thể phá vỡ cấu trúc, làm mất tính hợp lệ của URL nên người ta sẽ mã hoá các ký tự đặc biệt thành `%_số đại diện cho ký tự trong bảng mã ASCII`. Việc mã hoá này khiến các ký tự đặc biệt không ảnh hưởng đến cấu trúc url, đồng thời giúp phòng tránh một số kiểu tấn công phổ biến.
