# Tìm hiểu về Java-bean ?

## Khái niệm

là các lớp thuần Java được sử dụng để thực hiện các thực thể trong chương trình java
Cần phải tuân thủ theo các quy tắc

- Là một public class
- Có một hàm khởi tạo không đối số

```sh
public Test()
{
}
```

- Nó phải được nối tiếp : theo thứ tự khởi tạo hay tuần tự hóa
- Phải có các thuộc tính private : bảo vệ bởi getter/ setter
- Getter/ setter phải đặt tên theo quy tắc

| Phương thức | Miêu tả                                     |
| ----------- | ------------------------------------------- |
| getName()   | field là name với kiểu dữ liệu khác Boolean |
| setName()   | field là name                               |
| isActive()  | field is isActive với kiểu dữ liệu Boolean  |
| setActive() | field is isActive                           |

## Ví dụ về Bean ?

```sh
public class User implements java.io.Serializable
{
private int id;
private String name;


    public User()
    {
    }
    
    public User(int id, String name)
     {
        this.id = id;
        this.name = name;
    }

    public int getId()
    {
        return id;
    }
    public String getName()
     {
        return name;
    }

    public void setId(int id)
     {
        this.id = id;
    }
    public void setName(String name)
     {
        this.name = name;
    }

}
```
