# Bắt đầu tạo pr spring

Chọn hệ quản trị, chọn ngôn ngữ, chọn bản spring boot, thêm dependencies
[start.spring.io](https://start.spring.io/) để tạo

- chọn Maven

- chọn Ngôn ngữ

- chọn Spring newest

- group: spring.api( tên package )

- artifact : demo ( tên dự án )

- name : demo

- description :

- build ra jar hay war : chạy tren tomcat,... chọn **war**

- bản java : java 17( tùy )

- dependecies : lombok( bắt buộc : cung cấp annotation ), spring web, connect db( driver sql ), bảo mật ( spring security ), jpa ( hiberate ), messaging

## Config application.properties

```sh
spring.application.name=base
server.port=8080
spring.datasource.url=jdbc:postgresql://localhost:5432/base
spring.datasource.username=postgres
spring.datasource.password=admin123
spring.datasource.driver-class-name=org.postgresql.Driver
spring.security.user.name=admin
spring.security.user.password=123
spring.security.user.roles=USER

```

> Thêm code để bỏ bảo mật login page

```sh
@SpringBootApplication(exclude={SecurityAutoConfiguration.class})
```
