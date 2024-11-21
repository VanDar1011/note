# Cấu hình prefix cho endpoint

Có thể cần trong main file

```sh
@EnableWebMvc
```

```sh
@Configuration
public class ApiPrefixConfig implements WebMvcConfigurer
{

    @Override
    public void configurePathMatch(PathMatchConfigurer configurer)
    {
        configurer.addPathPrefix("/api", HandlerTypePredicate.forAnnotation(RestController.class));
    }

}
```
