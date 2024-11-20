# Đây là cơ chế bắt các microservice con với eureka

## Eureka Server

Tạo ra một server

Cấu hình in main @EnableEurekaServer

```sh
<dependency>
<groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

Cấu hình in application.properties

```sh
eureka.client.registerWithEureka = false
eureka.client.fetchRegistry = false
server.port = 8761
```

## Eureka Client

Tạo ra một và client

Cấu hình in main @EnableDiscoveryClient

```sh
<dependency>
<groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

Cấu hình in application.properties

```sh
eureka.client.serviceUrl.defaultZone  = http://localhost:8761/eureka
eureka.client.instance.preferIpAddress = true
spring.application.name = eurekaclient
```

## Cấu hình router động ( api getway )

```sh
@Bean
public RouteLocator myRoutes(RouteLocatorBuilder builder) 
{
return builder.routes()
.route(p -> p
.path("/\*\*")
.filters(f -> f.addRequestHeader("Src", "Tutorialspoint"))
.uri("http://localhost:8080/"))
.build();
}
```

```sh
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```

Cấu hình in application.properties

```sh
spring.application.name=gateway
server.port = 8111
```
