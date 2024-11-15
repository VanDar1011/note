# Tìm hiểu về cơ chê lập lịch va chạy bất đồng bộ

## Tìm hiểu về lập lịch

```sh
@Configuration
@EnableScheduling
public class SpringConfig
{
    ...
}
```

- @Schedule(...) : để lập lịch

- fixedDelay : là khoảng cách giữa hai lần chạy là khoảng thời gian

- fixedRate : là mỗi lần chạy các nhau là khoảng thời gian và đang là đơn luồng, có thẻ phải trong hàng đợi

- Lần đầu tiên sẽ chạy theo initialDelay, và sau đó sẽ chạy theo fixedDelay

```sh
@Scheduled(fixedDelay = 1000, initialDelay = 1000)
public void scheduleFixedRateWithInitialDelayTask()
{

    long now = System.currentTimeMillis() / 1000;
    System.out.println(
      "Fixed rate task with one second initial delay - " + now);
}
```

- cron = "0 15 10 15 \* ?" : là một biểu thức chạy crontab theo một khoảng thời gian nhất định

┌───────────── second (0-59)
│ ┌───────────── minute (0 - 59)
│ │ ┌───────────── hour (0 - 23)
│ │ │ ┌───────────── day of the month (1 - 31)
│ │ │ │ ┌───────────── month (1 - 12) (or JAN-DEC)
│ │ │ │ │ ┌───────────── day of the week (0 - 7)
│ │ │ │ │ │ (0 or 7 is Sunday, or MON-SUN)
│ │ │ │ │ │

x x x x x x

Cấu hình số lượng luồng để chạy Lập lịch

```sh
@Bean
public TaskScheduler  taskScheduler()
{
    ThreadPoolTaskScheduler threadPoolTaskScheduler = new ThreadPoolTaskScheduler();
    threadPoolTaskScheduler.setPoolSize(5);
    threadPoolTaskScheduler.setThreadNamePrefix("ThreadPoolTaskScheduler");
    return threadPoolTaskScheduler;
}
```

## Bất đồng bộ

@Configuration trước
Cũng phải cấu Hình @EnableAsync

@Async

Thay vì TaskScheduler thì TaskExcutor
