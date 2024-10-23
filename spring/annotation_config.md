# Tim hiểu về annotation trong @Configuration

Annotation này được đặt trong các method trong @Service

## @PreAuthorize: sẽ check trước rồi mới thực hiện method

```sh
@PreAuthorize("hasRole('ADMIN')")
Method_Name
```

## @PostAuthorize: sẽ thực hiện hàm xong, sau mới mới check xem có nên trả về hay không

```sh
@PostAuthorize("hasRole('ADMIN')")
Method_Name
```
