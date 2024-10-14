# Annotation in project

## @NoargsContructor

Sinh ra constructor mặc định không tham số

## @RequiredArgsConstructor

Sinh ra một constructor với các tham số bắt buộc phải có giá trị

sẽ không sinh các tham số trong constructor đối với các thuộc tính:

1. Non-final

2. Thuộc tính final đã được khởi tạo

3. Thuộc tính static

4. Các thuộc tính @NonNull đã được khởi tạo

Mặc định sẽ la là public, để nó trở thành private sử dụng _access = AccessLevel.PRIVATE_

@RequiredArgsConstructor(onConstructor = @\_\_(@Autowired)) tự động inject

## Getter , setter

Phương thức mặc định là public, tạo getter, setter, để mức class sẽ toàn bộ, để mức filed sẽ filed

@Getter(AccessLevel.NONE) loaị bỏ getter, hoặc setter đó

Thay mức độ truy cập khác tương ứng

## @Data

Bao gồm cả getter và setter

## @Column : k cần đặt tên nếu trùng

## @GeneratedValue

Mặc định là auto

```sh
 @Id

    @GeneratedValue(generator = "sequence-generator")

    @GenericGenerator(

      name = "sequence-generator",

      strategy = "org.hibernate.id.enhanced.SequenceStyleGenerator",

      parameters =
      {

        @Parameter(name = "sequence_name", value = "user_sequence"),

        @Parameter(name = "initial_value", value = "4"),

        @Parameter(name = "increment_size", value = "1")

        }

    )

    private long userId;
```

## @Transaction

Vị trí : trên lớp hoặc trên method, định nghĩa interface

Thứ tự ghi đè : _giao diện, siêu lớp, lớp, phương thức giao diện, phương thức siêu lớp và phương thức lớp._

Đảm bảo tính toàn vẹn dữ liệu khi có lỗi xảy ra, tư động commit hoặc rollback

@Transactional(rollbackFor = Exception.class) : check nếu có checked exception

1. propagation transaction

_REQUIRED ( default ) _: nếu có đã có giao dịch, sử dụng giao dịch đó, nếu không thì tạo mới

_REQUIRES_NEW_ : bắt buộc tạo mới

_SUPPORTS_ : Nếu có giao dịch thì giao dịch đó sẽ được dùng, nếu không có giao dịch, phương thúc sẽ không chạy trong một giao dịch

_MANDATORY_: Phải có một giao dịch đang tồn tại, nếu không sẽ ném ra ngoại lệ.

_NEVER_: Phương thức không bao giờ được chạy trong một giao dịch, nếu có sẽ ném ra ngoại lệ.

2. isolation : Đặt mức độ cách li

_READ_UNCOMMITTED_: Cho phép đọc dữ liệu chưa được commit, dễ dẫn đến lỗi "dirty read".

_READ_COMMITTED_: Không cho phép đọc dữ liệu chưa được commit, chỉ đọc dữ liệu đã commit.

_REPEATABLE_READ_: Đảm bảo rằng dữ liệu được đọc sẽ không bị thay đổi bởi các giao dịch khác trong suốt thời gian của giao dịch.

_SERIALIZABLE_: Mức cách ly cao nhất, đảm bảo rằng các giao dịch được thực thi một cách tuần tự.
