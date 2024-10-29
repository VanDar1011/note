# Làm việc với file xml để cấu hình bean

- Bean được quản lí bởi JSF( java server faces ), tham chiếu bởi file .xhtml

- Bean được quản lí bởi ioc Container ( invension of control container ): spring container : quản lí sự khởi tạo, cấu hình, vòng đời

## Khai báo bean

Khi khái báo như thế sẽ làm mọi @Bean

```sh
 default-init-method = "init"
   default-destroy-method = "destroy">
```

```sh
<?xml version = "1.0" encoding = "UTF-8"?>

<beans xmlns = "http://www.springframework.org/schema/beans"
   xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation = "http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

   <!-- A simple bean definition -->
   <bean id = "..." class = "...">
      <!-- collaborators and configuration for this bean go here -->
   </bean>

   <!-- A bean definition with lazy init set on -->
   <bean id = "..." class = "..." lazy-init = "true">
      <!-- collaborators and configuration for this bean go here -->
   </bean>

   <!-- A bean definition with initialization method -->
   <bean id = "..." class = "..." init-method = "...">
      <!-- collaborators and configuration for this bean go here -->
   </bean>

   <!-- A bean definition with destruction method -->
   <bean id = "..." class = "..." destroy-method = "...">
      <!-- collaborators and configuration for this bean go here -->
   </bean>

   <!-- more bean definitions go here -->

</beans>
```

> lazy-init : sẽ trì hoãn việc tạo cho tới khi được yêu cầu đầu tiên

> init-method: sẽ gọi phương thức khi bean được tạo, cách khác sử dụng @PostContructor hoặc @Bean(initMethod = "initialize")

Có thể sử dụng

```sh
implement InitializingBean
{
    public void afterPropertiesSet()
    {
    // do some initialization work
    }
}
```

> destroy-method: sẽ gọi phương thức khi bean được phá hủy, cách khác sử dụng @PreDestroyed hoặc @Bean(destroyMethod = "cleanup")

Có thể sử dụng

```sh
implements DisposableBean
{
   public void destroy()
    {
      // do some destruction work
   }
}
```

Test phá hủy Bean

```sh
context.registerShutdownHook();
```

## Bean có thể có nhiều phạm vi khác nhau (scope), chẳng hạn như:

\*\*
_Singleton:_ Mặc định, chỉ một instance duy nhất được tạo ra và chia sẻ.

_Prototype_: Mỗi lần yêu cầu bean, một instance mới được tạo ra.

_Request_: Một instance được tạo cho mỗi yêu cầu HTTP (chỉ dành cho web).

_Session_: Một instance được tạo cho mỗi phiên làm việc (chỉ dành cho web).

_Global Session_: Tương tự như session nhưng cho các ứng dụng portlet.
\*\*

## BeanPostProcessor: Can thiệp vào vòng đời @Bean

```sh
package com.tutorialspoint;

import org.springframework.beans.factory.config.BeanPostProcessor;
import org.springframework.beans.BeansException;

public class InitHelloWorld implements BeanPostProcessor
{
public Object postProcessBeforeInitialization(Object bean, String beanName)
throws BeansException
{

      System.out.println("BeforeInitialization : " + beanName);
      return bean;  // you can return any other object as well

}
public Object postProcessAfterInitialization(Object bean, String beanName)
throws BeansException
{

      System.out.println("AfterInitialization : " + beanName);
      return bean;  // you can return any other object as well

}
}

```

Thêm vào file xml

```sh
<bean class = "com.tutorialspoint.InitHelloWorld" />
```

## @ManagedBean để định nghĩa bean được đăng kí và quản lí với jsf famework

You can specify the scope of the managed bean using the @ManagedProperty annotation. Common scopes include:

> @SessionScoped: The bean is available for the duration of the user session.

> @RequestScoped: The bean is created and available only for a single HTTP request.

> @ViewScoped: The bean is available for the duration of a JSF view.

> If no scope is specified, the default is @RequestScoped.

## @ComponentScan

Annotation để import thêm Bea Bean vào

```sh
@Component({"com.viettel.web","com.viettel.fw"})
```

## @Import thay cho @ComponentScan

```sh
@Import(VehiclePartSupplier.class)
class VehicleFactoryConfig {}
```

## @ImportResource

```sh
@Configuration
@ImportResource("classpath:/annotations.xml")
class VehicleFactoryConfig {}
```

## @PropertySource

```sh
@PropertySource("classpath:/annotations.properties")
```

## @PropertySources

```sh
@PropertySources(
{
@PropertySource("classpath:/annotations.properties"),
@PropertySource("classpath:/vehicle-factory.properties")
}
)
```
