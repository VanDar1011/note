# Tìm hiểu về Anotation trong java

## Định nghĩa

> là một dạng chú thich hoặc một dạng siêu dữ liệu

Cung cấp thông tin cho mã nguồn Java
Có thể chú thích lớp, phương thức, biến, gói, tham số

- intergated anotaion
- defined anotaion

Các loại cơ bản như:

> @Deprecated
> @Overide
> @SuppersWarnings

Giúp chỉ dẫn trình biên dịch

## Mục đích

1. Chỉ đẫn trình biên dịch (complider)
2. Chỉ dẫn trong thời điểm biên dịch ( build-time)
3. Chỉ dẫn trong thời gian chạy ( run-time)

Không là các chú thích thuần túy, thay đổi cách trình biên dịch xử lí chương trình

## Chi tiết

@Overide : khi ghi đè phương thức, trình biên dịch sẽ báo lỗi nếu không ghi đè đúng

@Deprecated: đánh dấu class, field và chỉ dẫn tốt nhất không nên sử dụng nữa

@SuppressWarnings: thông báo cho trình biên dịch không in ra câu cảnh báo đó

> ("depracated") : hiển thị khi sử dụng

> ("unchecked") : hiển thị ép kiểu không an toàn

> ("rawtypes") : cảnh báo lỗi trong khai báo kiểu dữ liệu

## Khai báo Anotation ?

- Có thân hàm
- Không có thân hàm
