# Chọn cơ sở dữ liệu

```sh
psql -d db_name -U user_name
```

# Xóa màn hình

```sh
\! cls
```

# Thoát

```sh
\q
```

# Kiểm tra phiên bản

```sh
select version();
```

# Liệt kê tất cả db

```sh
\l
```

# Chọn db

```sh
\c db_name;
```

# Liệt kê bảng có sẵn

```sh
\dt;
```

# Liệt kê bảng chi tiết

```sh
\d;
```

# Liệt kê cụ thể một bảng

```sh
\d bills;
```

# Liệt kê tất cả Schema

```sh
\dn;
```

# Liệt kê tất cả views

```sh
\dv;
```

# Liệt kê tất cả function

```sh
\df
```

# Liệt kê tất cả user

```sh
\du;
```

# Thực thi sql và từ file

```sh
\i 'file_path';
```

Đã test

#

```sh
\o 'file_path';
command
\o
```

Đã test

# Bật timing : 2 lần để tắt

```sh
\timing
```

# Lấy kiểu html format : 2 lần để tắt

```sh
\H
```

# Thực thi lệnh trước đó

```sh
\g
```

# Bỏ căn lề

```sh
\a
```

# Để help

```sh
\h;
```

# Liệt kê tất cả

```sh
\?
```

# Cấu hình schema với log

```sh
db.driver: org.postgresql.Driver
db.url: jdbc:postgresql://localhost:5432/ax2012_1
db.username: my_user_name
db.password: my_password

spring.datasource.url= jdbc:postgresql://localhost:5432/ax2012_1
spring.datasource.username=my_user_name
spring.datasource.password=my_password
spring.datasource.schema=dbo

spring.jpa.hibernate.ddl-auto=validate

# Hibernate
hibernate.dialect: org.hibernate.dialect.PostgreSQLDialect // ngôn ngữ giao tiếp
hibernate.show_sql: true // show to debugging
hibernate.hbm2ddl.auto: update // update schema
entitymanager.packagesToScan: com.mycompany.myproduct.data // mapping
```
