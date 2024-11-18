# Triển khai interceptor : đánh chặn trước khi gửi request tới controller , và trước khi gửi phản hồi tới client

Class tạo @Component và implement HandleInterceptor

- preHandle() : hoạt động trước khi gửi request tới controller

- postHandle() : hoatj sống trước khi gửi response tới client

- afterCompletion() : su khi hoàn thành request và response

```sh
@Component
public class ProductServiceInterceptor implements HandlerInterceptor
{
   @Override
   public boolean preHandle(
      HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception
    {

      return true;
    }
   @Override
   public void postHandle(
      HttpServletRequest request, HttpServletResponse response, Object handler,
      ModelAndView modelAndView) throws Exception
      {

      }

   @Override
   public void afterCompletion(HttpServletRequest request, HttpServletResponse response,
      Object handler, Exception exception) throws Exception
      {

      }
}
```

Đăng kí Interceptor với InterceptorRegistry bởi dùng WebMvcConfigurer

```sh
@Component
public class ProductServiceInterceptorAppConfig implements WebMvcConfigurer
{
   @Autowired
   ProductServiceInterceptor productServiceInterceptor;

   @Override
   public void addInterceptors(InterceptorRegistry registry)
   {
      registry.addInterceptor(productServiceInterceptor);
   }
}
```
