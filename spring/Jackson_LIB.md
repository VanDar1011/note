# Thư viện Jackson chuyển đổi từ đối tượng Java sang dạng dữ liệu trả về

Chuyển đối tượng Java thành JSON (Serialization).

Chuyển JSON thành đối tượng Java (Deserialization).

```sh
CustomDateSerializer.class) và @JsonDeserialize(using = CustomDateDeserializer.class) trên field expiredDate.
```

Tùy chỉnh cách serialize và deserialize thông qua annotations.

Chuyển đổi đối tượng thành JSON

```sh
 User user = new User("John", 30);

        // Khởi tạo ObjectMapper
        ObjectMapper objectMapper = new ObjectMapper();

        // Chuyển đối tượng Java thành JSON
        String jsonString = objectMapper.writeValueAsString(user);
        System.out.println(jsonString);
```

Khi chuyển JSON thành đối tượng

```sh
String jsonString = "{\"name\":\"John\",\"age\":30}";

        // Khởi tạo ObjectMapper
        ObjectMapper objectMapper = new ObjectMapper();

        // Chuyển JSON thành đối tượng Java
        User user = objectMapper.readValue(jsonString, User.class);
        System.out.println("Name: " + user.getName());
        System.out.println("Age: " + user.getAge());
```

Điều chỉnh khi tên thuộc tính và field không khớp

```sh
@JsonProperty("username")
```

Loại bỏ ra khoiar dữ liệu trả về

```sh
@JsonIgnore
```

Định dạng dữ liệu trả về

```sh
@JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")
```

Chỉ định thứ tự của dữ liệu trả về

```sh
@JsonPropertyOrder({ "name", "id" })
```

Bọc một tên wrapper

```sh
@JsonRootName(value = "root")
MyBean bean = new MyBean(1, "My bean");
```

@JsonGetter để chỉ định một phương thức để lấy giá trị cho thuộc tính

```sh
String result = new ObjectMapper().writeValueAsString(bean);
// {"id":1,"name":"My bean"}
```
