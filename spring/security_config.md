# Cấu hình Security cho ứng dụng

```sh

@Configuration
@EnableWebSecurity
public class SecurityConfig
{
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception
     {
        http
                .authorizeHttpRequests((httpRequest) -> httpRequest.requestMatchers("/**").permitAll()

                )
                .rememberMe(Customizer.withDefaults())
                .httpBasic(withDefaults());
        return http.build();
    }
}

```

> permitAll() : để cho phép tất cả

> .anyRequest().authenticated() : để bắt xác thực tất cả các request còn lại không khớp của permitAll()

# BCryptPasswordEncoder

## Mã hóa

```sh
BCryptPasswordEncoder encoder = new BCryptPasswordEncoder(16);
encoder.encode("password");
```

## Kiểm tra password có match

```sh
encoder.matches("plaintext","crypto_pass");
```

# Argon2PasswordEncoder

## Mã hóa

```sh
Argon2PasswordEncoder encoder = Argon2PasswordEncoder.defaultsForSpringSecurity_v5_8();
encoder.encode("password");
```

## Giải mã

```sh
encoder.matches("plaintext","crypto_pass");
```

# Pbkdf2PasswordEncoder

## Mã hóa

```sh
Pbkdf2PasswordEncoder encoder = Pbkdf2PasswordEncoder.defaultsForSpringSecurity_v5_8();
String result = encoder.encode("myPassword");
```

# SCryptPasswordEncoder

## Mã hóa

```sh
SCryptPasswordEncoder encoder = SCryptPasswordEncoder.defaultsForSpringSecurity_v5_8();
String result = encoder.encode("myPassword");
```

## Giải mã

```sh
encoder.matches("plaintext","crypto_pass");
```
