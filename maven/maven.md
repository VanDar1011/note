# Maven là gì ?

## Định nghĩa

**Maven** là trình quản lí thư viện
packaging

**jar -> destop**

**pom -> web**

**war -> web**

_GroupId_ : tên công ty

_Artifactid_ : tên của project name

Thư mục _main/java_ là chứa code

Thư mục _main/resouce_ chứa tài nguyên

## Cách import thư viện

> Trong file pow.xml, lấy dependency từ [maven response](https://mvnrepository.com/)

```sh
<dependencies>
	<dependency>
		<groupId>org.postgresql</groupId>
		<artifactId>postgresql</artifactId>
		<version>42.7.4</version>
	</dependency>
	<dependency>
		<groupId>junit</groupId>
		<artifactId>junit</artifactId>
		<version>4.13.2</version>
		<scope>test</scope>
	</dependency>
</dependencies>
```
