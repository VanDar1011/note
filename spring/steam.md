# Tìm hiểu về Stream

Stream filter( function ) : trả về mảng mới nếu function trả về true

Stream map ( function ) : chuyển đổi phần từ sang dạng khách

Stream flatMap() : chuyển đổi mỗi phần tử thành một steam, sau đó hợp nhất lại

void forEach() : thực thi một hành động cho mỗi phần sử

type_Collections collect() : chuyển đổi thành dạng khác

```sh
Collectors.toList()
```

unique_Value reduce(innit, function): trả về một giá trị duy nhất

Stream distinct() : loại bỏ phần tử trùng

Stream sorted() : sắp xếp theo tự nhiên

Stream limit(long maxsize) : giới hạn số lượng phần tử

Stream skip() : bỏ qua một số phần tử đầu tiên

boolean anyMatch(function) : xem có phần tử thỏa mãn không
