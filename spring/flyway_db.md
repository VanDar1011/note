# FlywayDB

## Khái niệm

là việc tích hợp database giống như sequelize-cli

## Cài đặt

Tải thư viện

```sh
<dependency>
    <groupId>org.flywaydb</groupId>
    <artifactId>flyway-core</artifactId>
    <version>10.21.0</version>
</dependency>
<dependency>
    <groupId>org.flywaydb</groupId>
    <artifactId>flyway-database-postgresql</artifactId>
    <version>10.21.0</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.7.4</version>
</dependency>
```

Thêm vài file application.properties

```sh
spring.flyway.enabled=true
spring.flyway.validate-on-migrate=true
spring.flyway.baseline-on-migrate = true
spring.flyway.baseline-version = 0
```

Tạo file dưới /src/main/resources/db/migration
File .sql sẽ tự động thêm và db
Đang bị xung đột db
