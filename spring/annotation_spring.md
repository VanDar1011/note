# Annotation cơ bản Spring boot

## @Autowire

Tự động nhúng các bean được Spring Container sinh ra vào các class được khai báo @Autowire

> Cơ chế khi Spring bắt đầu chạy nó sẽ quét qua các lớp có sử dụng annotation để tạo Bean

> Đồng thời sẽ tìm kiếm xem trong các bean đó có khai báo @Autowire không, nó sẽ tìm kiếm Bean tương ứng để tiêm( Injection ) vào bean đó

```sh
//Properties
@Service
public class UserService
{

        @Autowired
        UserRepository userRepository;

        @Autowired
        FacebookUtil facebookUtil;
}
```

## @Configuration

Được sử dụng để chỉ ra rằng, Class khai báo sử dụng @Configure sẽ khai báo một hoặc nhieuf @Bean method trong class đó

> Thông thường các @Bean cấu hình trong dự án ta sẽ để trong các lớp configuration này. Ví dụ cấu hình Elasticsearch, Thymeleaf, đa ngôn ngữ,…

## @Bean

Đánh dấu trên method thông báo cho Spring, method đó sẽ sinh ra một bean và được quản lí bởi Spring Container.

Bean annotation có thể sử dụng với các tham số như name, initMethod hoặc destroyMethod

> Tất cả các Method sử dụng annotation @Bean phải nằm trong class Configuration.

```sh
@Configuration
public class WebDriverConfig
{

    @Bean
    public WebDriver Chrome()
    {
        System.setProperty("webdriver.chrome.driver", "/Downloads/chromedriver_linux64/chromedriver");
        return new ChromeDriver();
    }
}
```

## @PreDetroy và @PostConstruct

Đây là cách dùng khác để quản lý vòng đời của Bean. Ngoài cách sử dụng initMethod và destroyMethod. Ta có thể sử dụng @PreDetroy và @PostConstruct với cùng một mục đích

```sh
public class Computer
{

    @PostConstruct
    public void turnOn()
    {
        System.out.println("Load operating system");
    }

    @PreDestroy
    public void turnOff()
    {
        System.out.println("Close all programs");
    }
}
```

## @ComponentScan

Sử dụng annotation này để thông báo cho spring container rằng: “Phải biết vào các package nào trong dự án để quét các Annotation và tạo Bean.”

```sh
@Configuration
@ComponentScan(basePackages = "minhchuan.spring ")
public class SpringComponentDemo
{
   // ...
}
```

## @Component

Khi một class sử dụng annotation này: “Thì sẽ được tạo thành 1 Bean, và tiêm vào các lớp nào cần dùng tới nó”

| Component | Configuration |
| --------- | ------------- |

| Sẽ không thể @Autowire một lớp nếu lớp đó không sử dụng @Component.  
Nó giống như file Bean.xml dùng để khai báo các bean. | Khi bạn muốn xác định lớp để Injection thì phải đánh dấu  
bằng cách sử dụng annotation này để Spring biết. Sẽ được Spring  
tự động phát hiện. |

## @Service

Annotation đặc biệt của @Componet để xử lí nghiệp vụ logic

```sh
@Service
public class UserService
{

    @Autowired
    UserRepository userRepository;

    @Autowired
    FacebookUtil facebookUtil;
}
```

## @Repository

Đây cũng là một annotation đặc biệt của @Component. Được dùng để thao các với cơ sở dữ liệu.

Jpa sẽ cung cấp cho các hàm select, update,... cơ bản. Có thể áp dụng thêm Query Creation.

Các Interface thường gặp: CrudRepository, JpaRepository, MongoRepository,...

```sh
@Repository
public interface UserRepository extends JpaRepository <User, Integer>
{
    //Query Creation
}
```

## @Scope

Đây là phạm vi Bean được sinh ra và bị phá hủy dưới sự quản lí của Spring Container. Khi Bean sinh ra có các phạm vi được sử dụng và các tùy chỉnh của nó:

- Singleton: Đây sẽ là scope mặc định của 1 bean khi được sinh ra. nó có nghĩa: “bean chỉ tạo 1 lần và sử dụng trong container. Chỉ duy nhất một bean tồn tại trong container”.

> Có nghĩa là tại 1 thời điểm Container chỉ load một Bean nhất định.

- Prototype: ngược lại với Singleton, ta muốn có nhiều Bean thì sử dụng scope này.

- Request: Bean được sinh ra thông qua các HTTP Request của người dùng. Chỉ được dụng trong các ứng dụng Web.

- Session: Bean được sinh ra thông qua các HTTP Session.

## @PropertySource & @Value

Chúng ta sử dụng @PropertySource để cho Spring biết tìm các file properties cấu hình cho hệ thống ở đâu.

Đồng thời sử dụng @Value để lấy giá trị trong file properties.

```sh
    @Configuration
    @PropertySource("classpath:application.properties")
    public class MongoDBConfiguration
    {

        @Value("${mongodb.url}")
        private String url;

        @Value("${mongodb.db}")
        private String name;
    }
```

## @Valid

Dùng để kiểm tra dữ liệu có đúng như mình mong muốn hay không.

```sh
@Entity
public class User
{

    @Id
    @GeneratedValue
    private Long id;

    @NotEmpty(message = "Please provide a name")
    private String name;

    @NotEmpty(message = "Please provide a className")
    private String className;

    //...
}

@RestController
public class UserController
{

    @PostMapping("/users")
    Book newBook(@Valid @RequestBody User user)
    {
        //...
    }

}
```

## @ReponseBody

Thông báo cho người dùng biết rằng APIở controller, sẽ trả về một đối tượng Object kiểu Json cho client chứ không render ra một trang view.

## Controller

Một class được đánh dấu là @Controller thì để khai báo Class đó là một controller và có nhiệm vụ mapping request trên url vào các method tương ứng trong controller. Ví dụ dưới đây mình khai báo Class HomeController là một Controller . Khi người dùng gõ vào http://localhost:8080/ thì sẽ được xử lý bởi Class HomeController. Như vậy nhiệm vụ của Controller là điều hướng các request (yêu cầu) người dùng vào method xử lý tương

```sh
@Controller
public class HomeController
{

    @RequestMapping("/")
    public String homePage()
    {
        return "home";
    }

}
```

## @RequestMapping

Có nhiệm vụ ánh xạ các request (yêu cầu) người dùng vào method tương ứng trong controller. Ví dụ : Khi ta nhập vào url là http://localhost:8080/method2 thì nó sẽ được xử lý bởi phương thức là public String method2().

Ví dụ : Khi ta nhập vào url là http://localhost:8080/method3 thì nó sẽ được xử lý bởi phương thức là public String method3().

```sh
@RequestMapping(value = "/method2", method = RequestMethod.POST)
    public String method2()
    {
        return "method2";
    }

@RequestMapping(value = "/method3", method = {RequestMethod.POST, RequestMethod.GET})
    public String method3()
    {
        return "method3";
    }
```

## PathVariable

@PathVariable được sử dụng để xử lý những URI động, có một hoặc nhiều parameter trên URI.

```sh
@RequestMapping("/test2/{id}/{name}")
public String test2(@PathVariable("id") int id, @PathVariable("name") String name, Model model)
{
  model.addAttribute("id", id);
  model.addAttribute("name", name);
  return "test2";
}
```

## @RequestParam

Chúng ta sử dụng @RequestParame để bắt các giá trị các tham số mà người dùng truyền vào trên url theo định dạng key và value.

Ví dụ mình có cái link sau http://localhost:8080/api/foos?id=abc . Bây giờ mình muốn lấy giá trị abc của tham số id trên url thì mình sẽ dùng @RequestParam . Ở đây mình khai báo giá trị tham số trên URL theo định dạng key = value (id=abc).

Chúng ta khai báo @RequestParame trong method getFoos(@RequestParam String id) . Như vậy biến id sẽ có giá trị là abc nhờ cơ chế mapping.

```sh
@GetMapping("/api/foos")
@ResponseBody
public String getFoos(@RequestParam String id)
{
    return "ID: " + id;
}
```

## @RequestBody

```sh
@RequestMapping(path = "/something", method = RequestMethod.PUT)
public void handle(@RequestBody String body, Writer writer) throws IOException
{
writer.write(body);
}
```

## @Required

Áp dụng cho method bean setter. Nó chỉ ra rằng bean được chú thích phải được điền vào thời điểm cấu hình thuộc tính bắt buộc, nếu không sẽ ném ra ngoài lệ BeanInitizationException

```sh
public class Machine
{
private Integer cost;
@Required
public void setCost(Integer cost)
{
this.cost = cost;
}
public Integer getCost()
{
return cost;
}
}
```

## GetMapping

## @PostMapping

## @PutMapping : sửa cả

## @DeleteMapping

## @PatchMapping : sửa 1 phần
