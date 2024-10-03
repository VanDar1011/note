# Tìm hiểu hiberate ?

## Khái niệm

Framework để kết nối đến với cơ sở dữ liệu

_ORM_ và _JPA_ và _Hibernate_

- Nhu cầu ánh xạ Các ResultSet sang Object

> ORM ( Object Relational Mapping ) : tiếp cận lấy dữ liệu hướng đối tượng

> JPA ( Java Persistence Api) : tiêu chuẩn kĩ thuật trong lĩnh vực phát triển ứng dụng java để lập trình đối tượng quan hệ (ORM)

> JPA là một tiêu chuẩn chỉ là interface, Hibernate là một triển khai của JPA

> HQL là ngôn ngữ truy vấn chuyển sang SQL để truy vấn giống như Sequelize

![](https://viettuts.vn/images/hibernate/kien-truc-hibernate.jpg)

## Chi tiết

JTA, JNDI : máy chủ ee

JDBC : kết nối cơ sở dữ liệu

Configuration : cấu hình kết nối

Session Factory

Session

Transaction : chuỗi truy vấn, rollback

Query : tương tác cơ sở dữ liệu
Criteria

HQL : lệnh riêng của Hibernate, làm việc với đối tượng Java thay vì bảng

Criteria : truy vấn để lọc và lấy dữ liệu từ cơ sở dữ liệu.

SQL : truy vấn

## Mapping

Mapping XML

- class

> <mapping class="com.hibernate.entities.User"></mapping>

- resource

> <mapping resource="User.hbm.xml"></mapping>

- add bằng code

Mapping Annotation XML

### @Entity là thực thể

Entity khớp với một bảng lấy tên theo thứ tự ưu tiên: nếu cái trên sai thì bắn lỗi ngay

1. name trong @Table

2. name trong @Entity

3. name của class

```sh
> @Entity(name = "users")

hoặc

> @Entity
> @Table(name="users")
```

### @Table là một bảng được map

### @Id

Chỉ định cột là khóa chính

### @GeneratedValue(strategy =type)

Thường sẽ chỉnh định cùng với khóa chính, xác định các tạo giá trị

### @Column cột của bảng

Chỉ định tên cột nào trong database map với tên field được chú thích. Nếu không chỉ định, Hibernate sẽ lấy tên filed map với tên cột trong database

```sh
@Column(name = "name", length = 20, nullable = false)
	private String name;
```

Tên filed không cần giống trong db nếu đã sử chú thích name trong @Column

### @Transient

Trường này k tồn tại trong database

### @Temporal

Sử dụng để chú thích cho cột dữ liệu ngày tháng và thời gian (date time).

Có 3 giá trị cho TemporalType:

- _TemporalType.DATE_ : chú thích cột sẽ lưu trữ ngày tháng năm (bỏ đi thời gian).

- _TemporalType.TIME_ : chú thích cột sẽ lưu trữ thời gian (Giờ phút giây).

- _TemporalType.TIMESTAMP_ : chú thích cột sẽ lưu trữ ngày tháng và cả thời gian.
