# Tìm hiểu về kiến trúc request - response

## Định nghĩa

Thông thường client sẽ gửi một request(yêu cầu) lên server, và server gửi môt response(phản hồi) về cho client

## Các thành phần chính

Thành phần cơ bản của mô hình

> Máy khách ( Client ) : Người dùng hoặc hệ thống gửi yêu cầu ( thông qua web, ứng dụng di động,..)
> Yêu cầu( Request ) : Dữ liệu được gửi từ máy khách lên máy chủ. Gồm tham số(chuỗi truy vấn), tiêu đề(headers), cookies, hoặc thành phần thân (body) chứa dữ liệu
> Máy chủ ( Server) : Hệ thống nhận yêu cầu, xử lí và gửi phản hồi
> Phản hồi ( Response ) : Dữ liệu được gửi cho máy khách từ máy chủ, bào gồm status, tiêu đề, cookies, data

- Cookies là lưu trên trình duyệt, khi gửi lên server thì sẽ gửi cookie, lấy cookie từ yêu cầu
- SetCookies từ response trả về cho client

EndPoint

- Phương thức : GET,POST, PUT, PATCH, DELETE
- PUT : Thay thế đối tượng mới, PATCH là thay thế đối tượng với Key mới gửi lên
- URL : địa chỉ để truy cập tài nguyên
- Tham số : query params hoặc body
