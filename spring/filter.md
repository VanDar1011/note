# Filter

# Đánh chặn trước khi gửi request tới controller , và trước khi gửi phản hồi tới client

# Vai trò của filter

- Thêm hoặc thay đồi header HTTP

- Kiểm tra quyền người dùng

- Ghi nhật kí hoạt động của người dùng

- Thống kê thời gian phản hồi của yêu cầu

Filter được gọi trước khi controller được gọi, còn interceptor được gọi sau

Hình ảnh demo
![](https://www.baeldung.com/wp-content/uploads/2021/05/filters_vs_interceptors.jpg)
