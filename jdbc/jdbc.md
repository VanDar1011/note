# Tìm hiểu về jdbc

## Khái niệm

JDBC : Java Database Connectivity

Thư viện hỗ trợ kết nối java với cơ sở dữ liệu

> Tạo kết nối
> Tạo câu lệnh sql
> Thực thi câu lệnh sql
> xem và sủa kết quả trên db

--> Ra ResultSet
Hình ảnh về cấu trúc JDBC
![](https://miro.medium.com/v2/resize:fit:1400/0*KECANDMUAt17hYkU)

## Thư viện JDBC

DriverManager: quản lí drivers
Driver: Kết nối với database server
Connection : Quản lí các kết nối
Statement: Quản lí các câu lệnh
ResultSet: Tập kết quả trả về
SQLException : Lỗi ngoại lệ sql

Khởi tạo một kết nối tới db thông qua driver

## Nhược điểm

Mỗi RDBC có một driver riêng
Kết quả trả về không phải là Object mà phải conver
Phải biết trước kiểu dữ liệu đầu ra ( cột tương ứng )

## Code

```sh
public static Connection getConnection()
{
	Connection connection = null;
	 try
     {
         // PostgreSQL connection URL format: jdbc:postgresql://host:port/database
         String url = "jdbc:postgresql://localhost:5432/base";
         String user = "postgres";
         String password = "admin123";

         // Establish the connection
		 // Nạp driver thủ công
		 Class.forName("org.postgresql.Driver");
         connection = DriverManager.getConnection(url, user, password);

         if (connection != null) {
             System.out.println("Connected to the PostgreSQL server successfully.");
         } else {
             System.out.println("Failed to make connection!");
         }

     } catch (SQLException e) {
         System.out.println("Connection failed. Error: " + e.getMessage());
     }
	 return connection;
}
```

sau khi đã kết nối được , tạo statemet để thao tác với database

```sh
Connection connection = JDBCConnection.getConnection();
			Statement statement = connection.createStatement();
			String sql = "SELECT * FROM users";
			ResultSet rs = statement.executeQuery(sql);
			while (rs.next()) {
				int id = rs.getInt("id");
				String name = rs.getString("name");
				System.out.println(id + name);
				User user = new User(id, name);
				System.out.println(user.toString());
			}
```

> hoặc sử dụng PreparedStatement

```sh
Connection connection = JDBCConnection.getConnection();
//			Statement statement = connection.createStatement();
			String sql = "SELECT * FROM users WHERE id = ?" ;
			PreparedStatement preparedStatement = connection.prepareStatement(sql);
			int idUser = 2;
			preparedStatement.setInt(1, idUser);
			ResultSet rs = preparedStatement.executeQuery();
			while (rs.next()) {
				int id = rs.getInt("id");
				String name = rs.getString("name");
				System.out.println(id + name);
				User user = new User(id, name);
				System.out.println(user.toString());
            }
```

Thao tác với database
1 Tạo kết nối
2 Tạo trạng thái
3 Gửi lệnh

- Transaction

Bảo vệ dữ liệu khi một unit luồng thực thi có lỗi, rẽ rollback

```sh
Connection con = JDBCConnection.getConnection();
	try
    {
		Statement statement1 = con.createStatement();
//		con.setAutoCommit(false);
//		Statement statement2 = con.createStatement();
		String sql1 = "INSERT INTO users(name) values('Đinh Thị Hà')";
		String sql2 = "DELETE FROM users WHERE col= 2";
		statement1.executeUpdate(sql1);
		statement1.executeUpdate(sql2);
//		con.commit();
	} catch (SQLException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
```

- Sử dụng batch : thực hiện nhiều câu lệnh sql trong một lần gọi tới cơ sở dữ liệu
  > Tương tự với preparedStatement

```sh
Connection con = JDBCConnection.getConnection();
	String sql1 = "INSERT INTO users(name) VALUES('Name 1')";
	String sql2 = "INSERT INTO users(name) VALUES('Name 2')";
	String sql3 = "INSERT INTO users(name) VALUES('Name 3')";
	try
    {
		Statement statement = con.createStatement();
		statement.addBatch(sql1);
		statement.addBatch(sql2);
		statement.addBatch(sql3);
        statement.executeBatch();
		statement.close();
		con.close();
	} catch (SQLException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
```

```sh
	String sql4 = "INSERT INTO users(name) VALUES(?)";
		PreparedStatement preparedStatement = con.prepareStatement(sql4);
		preparedStatement.setString(1, "Name 5");
		preparedStatement.addBatch();
		preparedStatement.setString(1, "Name 6");
		preparedStatement.addBatch();
		preparedStatement.executeBatch();
		preparedStatement.close();
```

- CallableStatement : gọi thủ tục trong database

```sh
public static void main(String[] args) throws SQLException
{
		ResultSet rs = null;
		CallableStatement callableStatement = null;
		Connection con = JDBCConnection.getConnection();
		callableStatement = con.prepareCall("{CALL find_user(?, ?)}");
		callableStatement.setString(1, "Name");
        callableStatement.registerOutParameter(2, Types.REF_CURSOR); // Đăng ký tham số con trỏ

        callableStatement.execute(); // Gọi thủ tục

        // Lấy con trỏ kết quả
        rs = (ResultSet) callableStatement.getObject(2);
		while (rs.next()) {
			int id = rs.getInt("id");
			String name = rs.getString("name");
			System.out.println(id + name);
			User user = new User(id, name);
			System.out.println(user.toString());
		}
	}
```
