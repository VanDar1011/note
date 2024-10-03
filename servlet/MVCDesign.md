# Tìm hiểu về MVC

M: Model : Class mô phỏng đối tượng trong chương trình

V: View : File.jsp trong chương trình
C: Controller: Các Servlet đóng vài đỏ đẩy request qua RequestDispathcer

Sử dụng forward, dùng file .jsp để tạo web động

```sh
package com.controller;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.model.User;
@WebServlet(urlPatterns = {"/hello", "/xinchao"})
public class HelloController extends HttpServlet
{
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException
{
	// TODO Auto-generated method stub
	String name = "Datngo";
	User user = new User("Nguyen Van Dat", "La Khe, Ha Dong, Ha Noi");
	req.setAttribute("name", name);
	req.setAttribute("u", user);
	RequestDispatcher requestDispatcher = req.getRequestDispatcher("index.jsp");
	requestDispatcher.forward(req, resp);
}
}
```
