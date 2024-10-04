# Tìm hiểu về Postgres

Mỗi bảng là một record

## Các câu lệnh cơ bản

> Tạo bảng

```sh

CREATE TABLE users (
    id INT,
    name VARCHAR(255),
)
```

> Chèn dữ liệu vào bảng

```sh
INSERT INTO users (name) VALUES("Nguyễn Văn Đạt")
```

> Lấy dữ liệu

```sh
SELECT * FROM users WHERE ...
```

> Thêm cột

```sh
ALTER TABLE users
ADD address TEXT;
```

> Sửa dữ liệu record

```sh
UPDATE users
SET name = 'Nguyễn Văn Đạt update'
WHERE id = 1;
```

> Thay đổi kiểu dữ liệu. Một vài cột không thể thay chuyển nếu cột có giá trị

```sh
ALTER TABLE users
ALTER COLUMN address TYPE VARCHAR(80);
```

> Xóa cột

```sh
ALTER TABLE users
DROP COLUMN adddress;
```

> Xóa bản ghi, k xóa cấu trúc bảng

```sh
DELETE FROM users
WHERE name = 'Nguyễn Văn Đạt update';
```

> Xóa bảng

```sh
DROP TABLE users;
```

## Toán tử

SELECT DISTINCT cột_lọc : LẤY MỘT BẢN GHI TRẢ VỀ GIÁ TRỊ KHÁC
