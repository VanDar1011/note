# Event & Listener

## Định nghĩa

Event: là thay đổi trên một đối tượng, từ đó sẽ gọi hàm của listener đẻ xử lí tác vụ liên quan đến sự thay đỏi đó. Ví dụ khởi tạo servlet, tạo session, tạo request

Listener: là interface có các hàm tương ứng với Event diễn ra để gọi

> Các hàm ở listener sẽ có các tham số là đối tượng Event tương ứng
> Cầm implement listener để viết logic cần thiết

Áp dụng để theo dõi trạng thái thay đổi của servlet context, session context , request context,..

## Servlet Context

- Theo dõi trạng thái của servlet khi được triển khai ( deploy) hay hủy ( destroy) lên server
- Sử dụng để cập nhật trạng thái, tạo cơ sở dữ liệu, bảng,..
- ServletContextEvent
- ServletContextListener : init, destroy cấu hình

```sh
@WebListener
public class MyContextListener implements ServletContextListener
{
    @Override
    public void contextInitialized(ServletContextEvent sce)
    {
        // Initialization code here
    }

    @Override
    public void contextDestroyed(ServletContextEvent sce)
    {
        // Cleanup code here
    }
}
```

- ServletContextAttributeEvent
- ServletContextAttibuteListener

```sh
@WebListener
public class MyContextAttributeListener implements ServletContextAttributeListener
{
    @Override
    public void attributeAdded(ServletContextAttributeEvent event)
    {
        System.out.println("Attribute added: " + event.getName() + "=" + event.getValue());
    }

    @Override
    public void attributeRemoved(ServletContextAttributeEvent event)
    {
        System.out.println("Attribute removed: " + event.getName());
    }

    @Override
    public void attributeReplaced(ServletContextAttributeEvent event)
    {
        System.out.println("Attribute replaced: " + event.getName() + "=" + event.getValue());
    }
}
```

## Servlet Session

- Theo dõi trạng thái của Session khi được tạo, xóa và thêm giá trị vào session
- Sử dụng để cập nhật trạng thái online, chống lại đăng nhập nhiều máy
- HttpSessionEvent
- HttpSessionListener
- HttpSessionBindingEvent
- HttpSessionAttibuteListener

> Triển khai session để theo dõi đăng nhập

```sh
public class LoginListener implements HttpSessionListener, HttpSessionAttributeListener
 {
	public static int onlineUser = 0;

	@Override
	public void sessionCreated(HttpSessionEvent se)
     {
		// TODO Auto-generated method stub
		onlineUser++;
		System.out.println("User Online : " + onlineUser);
	}

	@Override
	public void sessionDestroyed(HttpSessionEvent se)
     {
		// TODO Auto-generated method stub
		onlineUser--;
		System.out.println("User Online : " + onlineUser);
	}
	@Override
	public void attributeAdded(HttpSessionBindingEvent event)
    {
		// TODO Auto-generated method stub
		if(event.getName().equals("loginUser")) {
			System.out.println("Login thêm");
		}
	}
	@Override
	public void attributeRemoved(HttpSessionBindingEvent event)
    {
		// TODO Auto-generated method stub
		if(event.getName().equals("loginUser")) {
			System.out.println("Login giảm đi");
		}
	}
}
```

Keyword: đếm xem bao người online, đếm xem bao nhiêu người vào cùng tài khoản

## Servlet request Event & Listener

- Theo dõi trạng thái của servlet request khi được tạo ra và kết thúc, cũng như thay đổi giá trị
- Sử dụng để theo dõi logs thời gian request
- ServletRequestEvent
- ServletRequestListener
- ServletRequestAttributeEvent
- ServletRequestAttributeListener
