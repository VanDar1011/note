# Tìm hiểu requestDispatcher

> Là **dispatcher** phía backend,
> **Redirect** là client gọi trực tiếp

forword là chuyển sang URL khác để thực hiện nội dung

![](https://d2jdgazzki9vjm.cloudfront.net/images/forward.JPG)

include là bao gồm gội dung của nó và thằng chuyển gộp lại

![](https://d2jdgazzki9vjm.cloudfront.net/images/include.JPG)

The main difference is that when you use forward the control is transferred to the next servlet/jsp you are calling, while include retains the control with the current servlet, it just includes the processing done by the calling servlet/jsp(like doing any out. println or other processing).

```sh
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException

{
		// TODO Auto-generated method stub
		resp.setContentType("text/html");
		PrintWriter out = resp.getWriter();
		String user = req.getParameter("username");
		if (user.equals("admin")) {
			RequestDispatcher dispatcher = req.getRequestDispatcher("/welcome");
			dispatcher.forward(req, resp);
		} else {
			out.println("User không chính xác");
			RequestDispatcher dispatcher = req.getRequestDispatcher("/form-login");
			dispatcher.include(req, resp);
		}
	}

```
