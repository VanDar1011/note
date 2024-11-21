# Admin Server để giúp giám sát các ứng dụng

## Phía quản trị

Thêm thư viện

```sh
<dependency>
   <groupId>de.codecentric</groupId>
   <artifactId>spring-boot-admin-starter-server</artifactId>
   <version>3.3.3</version>
</dependency>
```

Thêm annotation vào main

```sh
@SpringBootApplication
@EnableAdminServer
public class AdminserverApplication
{
   public static void main(String[] args)
   {
      SpringApplication.run(AdminserverApplication.class, args);
   }
}
```

## Phía Client

Thêm thư viện

```sh
<dependency>
   <groupId>de.codecentric</groupId>
   <artifactId>spring-boot-admin-starter-client</artifactId>
</dependency>
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Thêm cấu hình trong file application.properties

```sh
spring.boot.admin.url = http://localhost:9090/
```
