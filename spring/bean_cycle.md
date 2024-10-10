# Vòng đời của @Bean

Gồm các bước sau:

- IoC container tạo bean bằng cách gọi constructor (có thể inject các bean dependency vào đây)

- Gọi các setter method để inject các bean vào bằng setter based injection

- Các method khởi tạo khác được gọi (không cần quan tâm nhiều)

- @PostConstructor được gọi

- Init method được gọi

Sau đó bean sẽ sẵn sàng hoạt động. Nếu sau đó bean không dùng nữa thì nó sẽ được hủy:

- Gọi @PreDestroy

- Hủy bean như các object thông thường

## @PostConstructor và @PreDestroy

> @PostConstruct là sau khi bean đã khởi tạo xong

> @PreDestroy là trước khi bean bị phá hủy

```sh
class Car
{
    @Autowired
    private final Engine engine;

    @PostConstruct
    public void testRun()
    {
        engine.run();
        engine.stop();
    }

    @PreDestroy
    public void stopEngine()
    {
        engine.stop();
    }
}
```
