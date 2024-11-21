# Gửi email

## Thêm thư viện

```sh
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

## ExampleCode : đã test oce

```sh
@Service
public class MailService
{
    public void sendmail() throws AddressException, MessagingException, IOException
    {
        Properties props = new Properties();
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.starttls.enable", "true");
        props.put("mail.smtp.host", "smtp.gmail.com");
        props.put("mail.smtp.port", "587");

        Session session = Session.getInstance(props, new javax.mail.Authenticator()
        {
            protected PasswordAuthentication getPasswordAuthentication()
            {
                return new PasswordAuthentication("datthao27042002@gmail.com", "gvqe phgx awae zznw");
            }
        });
        Message message = new MimeMessage(session);
        message.setFrom(new InternetAddress("datthao27042002@gmail.com"));
        message.setRecipients(
                Message.RecipientType.TO, InternetAddress.parse("datvu871@gmail.com"));
        message.setSubject("🎉🌟 Beautiful HTML Email with Icons, Styles & More! 🚀✨");

        message.setSentDate(new Date());

        // Create the HTML content with more icons
        String htmlContent = """
            <html>
                <head>
                    <style>
                        body { font-family: Arial, sans-serif; background-color: #f4f4f9; color: #333; padding: 20px; }
                        h1 { color: #4CAF50; }
                        p { font-size: 16px; line-height: 1.6; }
                        .button {
                            display: inline-block;
                            background-color: #4CAF50;
                            color: white;
                            padding: 10px 20px;
                            text-decoration: none;
                            border-radius: 5px;
                            font-size: 16px;
                        }
                        .footer { font-size: 14px; color: #777; text-align: center; padding: 10px 0; }
                    </style>
                </head>
                <body>
                    <h1>Welcome to Our Service! 🎉</h1>
                    <p>Hello, this is an example of a <strong>beautifully styled HTML email</strong> with icons and more advanced formatting. 🚀✨</p>
                    <p>We're excited to have you with us. Here's a special offer just for you:</p>
                    <p><strong>Exclusive Deal: 50% off</strong> on your first purchase! 🎁🛍️</p>
                    <p>Click the button below to claim your offer:</p>
                    <a href="http://localhost:8888/api/products_test" class="button">Claim Offer 🤑</a>

                    <p>Best regards, <br> Your Application Team 💼</p>

                    <div class="footer">
                        <p>Sent by Your Application &copy; 2024 | All rights reserved. 🔒</p>
                    </div>
                </body>
            </html>
        """;

        // Set the email content to HTML
        message.setContent(htmlContent, "text/html");

        // Send the email
        Transport.send(message);

//        System.out.println("Email sent successfully.");
    }
}
```
