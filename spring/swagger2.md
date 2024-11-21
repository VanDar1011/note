# Tìm hiểu về swagger2

## Khái niệm

Cung cấp giao diện truy cập api

## Cài đặt

Thêm thư viện

```sh
<dependency>
   <groupId>io.springfox</groupId>
   <artifactId>springfox-swagger2</artifactId>
   <version>2.7.0</version>
</dependency>
<dependency>
   <groupId>io.springfox</groupId>
   <artifactId>springfox-swagger-ui</artifactId>
   <version>2.7.0</version>
</dependency>
```

Thêm annotation @EnableSwagger2

```sh
@SpringBootApplication
@EnableSwagger2
public class SwaggerDemoApplication
{
   public static void main(String[] args)
   {
      SpringApplication.run(SwaggerDemoApplication.class, args);
   }
}
```

Tiếp theo, tạo Docket Bean để cấu hình Swagger2 cho ứng dụng Spring Boot của bạn. Chúng ta cần xác định gói cơ sở để cấu hình REST API(s) cho Swagger2.

```sh
@Bean
   public Docket productApi()
   {
      return new Docket(DocumentationType.SWAGGER_2).select()
         .apis(RequestHandlerSelectors.basePackage("com.tutorialspoint.swaggerdemo")).build();
   }
```

Cấu hình đã oci: project demo
