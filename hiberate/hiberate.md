# Tìm hiểu hiberate ?

## Khái niệm

**POJO** là viết tắt của **Plain Old Java Object**, một POJO là một class Java thuần không extend và không implement bất kỳ class hoặc interface nào trong project Java.

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

### 1.@Entity là thực thể

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

### 2.@Table là một bảng được map

### 3.@Id

Chỉ định cột là khóa chính

Khoá chính có thể là một trường hoặc nhiều trường kết hợp lại

### 4.@GeneratedValue(strategy =type)

Thường sẽ chỉnh định cùng với khóa chính, xác định các tạo giá trị

> GenerationType.AUTO : Column được đánh dấu bởi @GeneratedValue(strategy= AUTO) sẽ được gán giá trị tự động, giá trị đó có thể được sinh ra bởi SEQUENCE hoặc tự tăng (Nếu cột này có kiểu IDENTITY). Nó phụ thuộc vào loại database.
> GenerationType.IDENTITY : Cột có kiểu IDENTITY chỉ được hỗ trợ bởi một vài loại cơ sở dữ liệu, không phải là tất cả, ví dụ MySQL, DB2, SQL Server, Sybase và PostgreSQL. Oracle không hỗ trợ cột kiểu này.
> GenerationType.SEQUENCE : SEQUENCE là một đối tượng trong cơ sở dữ liệu, lưu trữ một giá trị tăng dần sau mỗi lần gọi nó để lấy giá trị tiếp theo, và được hỗ trợ bởi Oracle, DB2, và Postgres.
> GenerationType.TABLE : tạo khóa custom
> GenerationType.UUID : 36 kí tự ngẫu nhiên

### 5.@Column cột của bảng

Chỉ định tên cột nào trong database map với tên field được chú thích. Nếu không chỉ định, Hibernate sẽ lấy tên filed map với tên cột trong database

```sh
@Column(name = "name", length = 20, nullable = false)
	private String name;
```

Tên filed không cần giống trong db nếu đã sử chú thích name trong @Column

### 6.@Transient

Trường này k tồn tại trong database

### 7.@Temporal

Sử dụng để chú thích cho cột dữ liệu ngày tháng và thời gian (date time).

Có 3 giá trị cho TemporalType:

- _TemporalType.DATE_ : chú thích cột sẽ lưu trữ ngày tháng năm (bỏ đi thời gian).

- _TemporalType.TIME_ : chú thích cột sẽ lưu trữ thời gian (Giờ phút giây).

- _TemporalType.TIMESTAMP_ : chú thích cột sẽ lưu trữ ngày tháng và cả thời gian.

### 8.@Lob

Chú thích cùng Column để nói rằng cột đó kiểu BLOB hoặc CLOB

- BLOD (Binaray Large Object) : lưu trữ số lượng lớn dữ liệu binary như data, ảnh, video, audio hoặc bất kì file binary

- CLOB (Character Large Object) : lưu trữ text lớn như text, xml hoặc json

Phần thử length trong @Column trong trường này sẽ quyết định nó map vào BLOB/ CLOB nào

## 9.@ManyToOne

Diễn tả mối quan hệ Nhiều - Một, thường được dùng với @JoinColumn

Hibernate có các công cụ cho phép tạo ra các lớp Entity từ các bảng trong DB và cũng cho phép tạo các bảng từ các lớp Entity, bao gồm giàng buộc giữa các bảng
@ForeignKey cho phép chỉ định rõ tên Foreginkey sẽ được tạo ra

### 9.1 FetchType.LAZy

Hãy tải dữ liệu một cách lười biếng, nghĩa là chỉ tải khi được gọi

### 9.1 FetchType.EAGER

Hãy truy vấn toàn bộ các cột của bảng liên quan

## 10. @OneToMany

@OneToMany mô tả quan hệ 1-N (Một – Nhiều). Nó là đảo ngược của @ManyToOne, và vì vậy nó dựa vào @ManyToOne để định nghĩa ra @OneToMany.

## 11. @OneToOne

@OneToOne mô tả quan hệ 1-1 (Một – Một).

## 12. @ManyToMany

@ManyToMany mô tả quan hệ N-N (Nhiều – Nhiều).

## 13.@OrderBy

@OrderBy được sử dụng để sắp xếp một danh sách, vì vậy nó có thể được sử dụng cùng với @OneToMany, @ManyToMany.
