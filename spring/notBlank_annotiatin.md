# @NotNull

Check nếu nó bị null

# @NotEmpty

Chuỗi trống, và danh sách rỗng

# @NotBlank

Check nếu nó chuỗi trống, chuỗi chỉ có các khoảng trắng

Example

Tên chuỗi = null;
@NotNull: false
@NotEmpty: false
@NotBlank: false

Tên chuỗi = "";
@NotNull: đúng
@NotEmpty : sai
@NotBlank: sai

Tên chuỗi = " ";
@NotNull: đúng
@NotEmpty : đúng
@NotBlank : sai

Tên chuỗi = "Câu trả lời tuyệt vời!";
@NotNull: true
@NotEmpty : true
@NotBlank : true
