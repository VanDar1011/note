# Tìm hiểu về Actuator

Đây dùng để thu thập và giám sát ứng dụng

```sh
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Tắt quản lí bảo mật trong file application.properties

```sh
# management.security.enabled = false
# management.port = 9000
// hoặc ( mỗi page viết một khác )
management.server.port=8090
// cổng để chạy actuator
management.endpoints.web.exposure.include=*
// kich hoạt tất cả endpoint
management.endpoint.shutdown.enabled=true
// cho phép chúng ta tắt ứng dụng
management.endpoint.health.show-details=always
// show detail
```

## Các đầu api cơ bản Actuator

> actuator/health : tình trạng của ứng dụng

> actuator/metrics : danh sách các metric.

> actuator/metrics /{path} : xem cụ thể

> actuator/beans : các bean được quản lí

> actuator/env : cung cấp thông tin môi trường mà ứng dụng đang chạy như phiên bản java, hệ điều hành của máy, …

> actuator/info : cung cấp thông tin tùy biến, mặc định là rỗng

> actuator/shutdown : end point này sẽ giúp bạn tắt ứng dụng.( POST METHOD )
