# Dùng để gọi api bên ngoài, cần cấu hình

```sh
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.reactive.function.client.WebClient;
import org.springframework.web.service.invoker.HttpServiceProxyFactory;
import org.springframework.web.service.invoker.WebClientAdapter;

@Configuration
public class ExternalApiClientConfig
{
    @Bean
    public ExternalApiClient externalApiClient(WebClient.Builder webClientBuilder)
    {
        WebClient webClient = webClientBuilder
                .baseUrl("http://api.example.com/external-api") // Đặt Base URL
                .build();

        WebClientAdapter adapter = WebClientAdapter.forClient(webClient);
        HttpServiceProxyFactory factory = HttpServiceProxyFactory.builder(adapter).build();

        return factory.createClient(ExternalApiClient.class);
    }

    @Bean
    public WebClient.Builder webClientBuilder() {
        return WebClient.builder();
    }
}

```

```sh
import org.springframework.web.service.annotation.GetExchange;
import org.springframework.web.service.annotation.HttpExchange;

@HttpExchange("/external-api")
public interface ExternalApiClient
{

    @GetExchange("/users/{id}")
    User getUserById(@PathVariable Long id);
}

```

```sh
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/local-api")
public class UserController
{

    private final UserService userService;

    public UserController(UserService userService)
    {
        this.userService = userService;
    }

    @GetMapping("/users/{id}")
    public User getUser(@PathVariable Long id)
     {
        // Gọi Service để lấy thông tin User từ API bên ngoài
        return userService.fetchUserById(id);
    }
}
```
