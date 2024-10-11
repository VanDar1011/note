# Các phương thức được cung cấp sẵn khi thao tác với cơ sở dữ liệu

Khởi tạo một Optional từ giá trị có thể có hoặc không có

## Create/ Update

S save(S entity): Lưu hoặc cập nhật một thực thể.

## Read

Optional<T> findById(ID id): Tìm kiếm thực thể theo ID.

List<T> findAll(): Trả về tất cả các thực thể.

List<T> findAllById(Iterable<ID> ids): Tìm kiếm tất cả các thực thể theo danh sách ID.

## Delete

void deleteById(ID id): Xóa một thực thể theo ID.

void delete(T entity): Xóa một thực thể.

void deleteAll(): Xóa tất cả các thực thể.

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
