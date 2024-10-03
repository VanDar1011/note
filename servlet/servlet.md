# Tìm hiểu về Servlet

## Servlet là gì ?

- Khái niệm
  Servlets là một phương thức độc lập trên các nền tảng, dựa trên các thành phần để xây dựng các ứng dụng trên web, mà loại bỏ các hạn chế của các chương trình CGI. Servlets có quyền truy cập tới toàn bộ Java APIs, bao gồm JDBC API.
  Java Servlets là các chương trình chạy trên một webserver hoặc một application server và thực hiện như
  **một tầng trung gian**
  giữa yêu cầu với database
  Sử dụng Servlets, bạn có thể thu thập **Input** từ người dùng thông qua form, hiển thị bản ghi(record) từ **DB** hoặc nguồn khác, và tạo các trang web động.
  Hiệu suất tốt : dùng thread cho mỗi request

  > Hình ảnh minh họa
  > ![](https://www.vietjack.com/servlets/images/servlet-arch.jpg)

- Nhiệm vụ của Servlets

Đọc dữ liệu hiển thị( explicit ) được gửi bởi CLient
Đọc dữ liệu yêu cầu HTTP ẩn ( implicit ) được gửi bởi Client bao gồm cookie, media
Xử lí dữ liệu và cho ra kết quả
Gửi dữ liệu hiển thị ( document) tới Client
Gửi phản hồi HTTP ẩn tới Client , thiết lâp cookie, caching

- Package trong Servlets

Java Servlets là các lớp trong java chạy bởi một Web Server mà có một trình thông dịch hỗ trợ Java Servlets
Servlets được tạo bởi **javax.servlet** và **javax.servlet.http** là một phiên bản mở rộng của thư viện lớp Java. Các lớp này triển khai Java Servlet và JSP

- Vòng đời của servlet
  Bắt đầu bằng phương thức init()

  > chỉ gọi một lần khi servlet được tạo, không gọi lại
  > khi có yêu cầu , một luồng mới sẽ được tạo ra

  Gọi phương thức service() để xử lí một yêu cầu client

  > phương thức chính để thực hiện thực sự

  Bị hủy bởi triệu hồi phương thức destroy()

> use Annatation

```sh
@WebServlet(urlPatterns= {"/xin-chao","/demo"})
public class DemoServlet  extends HttpServlet
{
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
	resp.setContentType("text/html");
	PrintWriter printWriter = resp.getWriter();
	printWriter.println("Xin chao moi nguoi den voi trang web");
	printWriter.close();

}
```

> method:req

getServerName()
getServletPath()
getHeaderNames()
getHeader(key)
getParams() use int endpoint or field form
getQueryString()

```sh
System.out.println("Phuong thuc cua request"  + req.getMethod());
	System.out.println(req.getServerName());
	System.out.println(req.getServletPath());
	Enumeration< String> keys = req.getHeaderNames();
	while(keys.hasMoreElements()) {
		String key = keys.nextElement();
		System.out.println(key +  ":"+ req.getHeader(key));
	}

```

> method:response

resp.setContentType(_"text/plain"_ -- _"text/html"_);

```sh
resp.setContentType("text/plain");
	PrintWriter printWrite = resp.getWriter();
	printWrite.println("<h1>Header 1</h1>");
	printWrite.println("<h3>Header 3</h3>");
```

- Servlet config

```sh

@WebServlet(urlPatterns = {"/text-config"},initParams =
{
		@WebInitParam(name="name",value="Hoc servlet")
})
public class ServletConfigDemo extends HttpServlet
{
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException
{
	// TODO Auto-generated method stub
	String name = super.getServletConfig().getInitParameter("name");
	resp.setContentType("text/html");
	PrintWriter printWriter = resp.getWriter();
	printWriter.println("Xin chao :"  + name);
  System.out.println(getServletConfig().getServletName());
}
}
```

```sh
  <servlet>
	<servlet-name>demo-config</servlet-name>
	<servlet-class>com.trungtamjava.ServletConfigDemo</servlet-class>
	<init-param>
	<param-name>name</param-name>
	<param-value>nguyen van dat</param-value>
	</init-param>
	</servlet>

```

- Mã code http resp

  > 100 : continute
  > 302 : found
  > 400 : bad request
  > 401 : unthoriad
  > 403 : forbidden
  > 404 : not found
  > 500 : intenal error
  > 200 : oce
  > 201 : created
  > Mã code ảnh hưởng kết quả trả về

- SendRedirect : chuyển hướng trang sang trang mới, thay thế url

```sh
resp.sendRedirect("https://chatgpt.com/c66fb6194-1b4c-8012-89c4-8bf5531ef719");
```

hoặc

```sh
resp.setStatus(resp.SC_MOVED_PERMANENTLY);
resp.setHeader("Location", "https://chatgpt.com/c/66fb6194-1b4c-8012-89c4-8bf5531ef719");
```

- Cookies là gì ?

Là một file text lưu phía trình duyệt của cliet
Lưu thông tin dạng pari value/key
Request sẽ gửi thông tin Cookies trong header
Java Servlet hỗ trợ HTTP cooki
Cookie có thời gian sống nhất định

> setCookie

```sh
Cookie cookie = new Cookie("userId","dat_kma1234");
cookie.setMaxAge(15);
resp.addCookie(cookie);
```

> getCookies

```sh
Cookie[] cookies= req.getCookies();
		if(cookies.length > 0) {
			for(Cookie c : cookies) {
				if(c.getName().equals("username")) {
					username = c.getValue();
				}
			}
		}
```

- Sessions

Duy trì trạng thái của dữ liệu người dùng
Có thời gian sống xác định
Quản lí bằng SessionManager
Lưu dưới dạng key/value trên server

Set ID vào cookie để nhận dạng
Set id vào trường ẩn trong form
URL Rewriting

HTTPSession là một interface trong Servlet giúp lưu trữ thông tin người dùng qua cac servlet khác nhau

```sh
HttpSession session = req.getSession();
```

> setSession

```sh
HttpSession httpSession = req.getSession();
httpSession.setAttribute("name", "nguyendat");
```

> getSession

```sh
HttpSession httpSession = req.getSession();
Object obj = httpSession.getAttribute("name");
```

> confiure timeout

```sh
<session-config>
<session-timeout>1</session-timeout>
</session-config>
```

- Filter

Đối tượng dùng để xử lí _request_ trước khi gọi tới _servlet đích_, và _response_ trả kết quả từ servlet
Dùng _nhiều filter_ một lúc
Dễ dàng tích hợp
Tác dụng : logging, check ip, nén file, validate dữ liệu

![](https://d2jdgazzki9vjm.cloudfront.net/images/filter.JPG)

- config web.xml

```sh
<filter>
<filter-name>logger</filter-name>
<filter-class>com.trungtamjava.filter.Logger</filter-class>
</filter>
<filter-mapping>
<filter-name>logger</filter-name>
<url-pattern>/login-session</url-pattern>
</filter-mapping>
```

- use Anotation

```sh
@WebFilter(urlPatterns = {"/name1","/name2"})

```

use filter moi request

```sh
@WebFilter(urlPatterns = {"/*"})
```

- code implement Filter

> code in Logger

```sh
package com.trungtamjava.filter;

import java.io.IOException;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;
@WebFilter(urlPatterns = {"/login-session","/logout"}) // use Anotation
public class Logger implements Filter
{
	@Override
	public void destroy()
	 {
		// TODO Auto-generated method stub
		Filter.super.destroy();
	}

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
			throws IOException, ServletException
			{
		// TODO Auto-generated method stub
		System.out.println("Thực hiện filter");
		// handle resquest
		// doFilter
		// handle response
//		System.out.println(request.getParameter("name"));
		chain.doFilter(request, response);
	}

	@Override
	public void init(FilterConfig filterConfig) throws ServletException
	{
		// TODO Auto-generated method stub
		Filter.super.init(filterConfig);
	}

}

```

- initParams : giữ giá trị sau mỗi lần filter

```sh
package com.trungtamjava.filter;

import java.io.IOException;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;
import javax.servlet.annotation.WebInitParam;
//@WebFilter(urlPatterns = {"/login-session","/logout"})
@WebFilter(urlPatterns = {"/*"},initParams = @WebInitParam(name="count",value = "100"))
public class Logger implements Filter
{
	private int count;
	@Override
	public void destroy()
	{
		// TODO Auto-generated method stub
		Filter.super.destroy();
	}

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
			throws IOException, ServletException
			{
		count ++;
		System.out.println(count);
		// TODO Auto-generated method stub
		System.out.println("Thực hiện filter");
		// handle resquest
		// doFilter
		// handle response
//		System.out.println(request.getParameter("name"));
		chain.doFilter(request, response);
		response.setContentType("text/plain");
	}

	@Override
	public void init(FilterConfig filterConfig) throws ServletException
	{
		String countS = filterConfig.getInitParameter("count");
		count = Integer.valueOf(countS);
		// TODO Auto-generated method stub
		Filter.super.init(filterConfig);
	}

}
```

- ServletContext

chia sẻ dữ liệu toàn bộ servlet

> set

```sh

pw.println("<h2>xin chao</h2");
getServletContext().setAttribute("name", "test context");

```

> get

```sh
String name = (String) getServletContext().getAttribute("name");
```

> config in web.xml

```sh
<context-param>
<param-name>jdbc</param-name>
<param-value>sql</param-value>
</context-param>
```

- auto refresh Servlet

use SetHeader to autoRefresh

```sh
resp.setHeader("Refresh","1");
```

- welcome file list

> file bắt đầu cho project

chỉnh một vài file mặc định trong web.html
giống như list gồm index.html, index.htm

- Handle Error

trong web.xml, cấu hình để lấy theo mã lỗi, hoặc lấy theo loại lỗi

```sh
<error-page>
	<error-code>404</error-code>
	<location>/handle-error</location>
	</error-page>
```

> hoặc

```sh
	<error-page>
		<exception-type>java.io.IOException</exception-type>
		<location>
			/handle-error</location>
	</error-page>
```
