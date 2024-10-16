# Tìm hiểu về optinal

## Trả về thực thể nhất định hoặc không có

Optinal <User> user = getUser;

Optinal.empty() : trả về một instance rỗng

user.isEmpty(); check nếu trống

user.isPresent(); check nếu có giá trị

user.ifPresent( function )
