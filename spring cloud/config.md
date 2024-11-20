# Config in Server and Client

## Config in Server

Dependece

```sh
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

Add @EnableConfigServer in Main

```sh
@SpringBootApplication
@EnableConfigServer
public class ConfigserverApplication
{
   public static void main(String[] args)
   {
      SpringApplication.run(ConfigserverApplication.class, args);
   }
}
```

File application.properties in server app

```sh
server.port = 8888
spring.cloud.config.server.git.uri=file:///E:/Dev/config/
```

Go to E:/Dev/config/ folder and run the following git command to initialize it as git repo.

```sh
git init
```

The code for config-client properties file is given below

```sh
welcome.message = Welcome to Spring cloud config server
```

## Conifig in Client

Add dependence

```sh
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

Add @RefreshScope

```sh
@SpringBootApplication
@RefreshScope
public class ConfigclientApplication
{
   public static void main(String[] args)
   {
      SpringApplication.run(ConfigclientApplication.class, args);
   }
}
```

File application.properties in client

```sh
spring.application.name = config-client
spring.config.import=optional:configserver:http://localhost:8888/
```

> Bây giờ client sẽ dùng được file cấu hình cho client của Server đã cấu hình thông qua server
