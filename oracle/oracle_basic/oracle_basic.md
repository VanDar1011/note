# Tìm hiểu về oracle_basic

> Tạo cột tạm thời cho _cột_ hoặc _bảng_

```sh
column_name as alias_name
```

```sh
table_name aliac_name
```

> Kết hợp ( nốt cột thành một ), nếu có _khoảng trống_ alias*name phải có dấu *"alias*name"*

> || 'character' || để cụ thể kí tự giữa hai bảng

```sh
SELECT contact_id, first_name || last_name AS NAME
FROM contacts
WHERE last_name = 'Anderson';
```

> AND : kết hợp điều kiện

> AND kết hợp với OR

(điều kiện 1 và điều kiện 2) hoặc (điều kiện 3)

(điều kiện 1 hoặc điều kiện 2) và (điều kiện 3)

= điều kiện 1 và điều kiện 3 hoặc điều kiện 2 và điều kiện 3

> BETWEEN VALUE1 AND VALUE2 : Tìm giá trị giữa hai giá trị

> Comparison Operator

=, <>, !=, > , >=, <, <=, in(),not, between, is null, is not null ,like , regexp_like, exists

> Chèn nhiều bản ghi vào bảng sử dụng INSERT ALL

```sh
INSERT ALL
  INTO suppliers (supplier_id, supplier_name) VALUES (1000, 'IBM')
  INTO suppliers (supplier_id, supplier_name) VALUES (2000, 'Microsoft')
  INTO customers (customer_id, customer_name, city) VALUES (999999, 'Anderson Construction', 'New York')
SELECT * FROM dual;
```

> Lấy bản ghi chung của hai truy vấn con

```sh
SELECT column_list FROM table1
INTERSECT
SELECT column_list FROM table2;
```

> Lấy bản ghi chỉ có ở tập hợp 1, không có ở tập hợp 2

```sh
SELECT column_list FROM table1
MINUS
SELECT column_list FROM table2;
```

> Subquery : Dạng truy vấn lồng

> Regexp_like

^ : kí tự đầu
$ : kí tự kết thúc

- : matches - nhiều
