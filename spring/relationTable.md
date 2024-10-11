# Tìm hiểu về mối quan hệ có thể có giữa các bảng

## CascaseType

CascadeType.ALL: It means that all operations are cascaded from the parent entity to the child entity.
CascadeType.PERSIST: When the parent entity is persisted (saved), the associated child entity will also be persisted.
CascadeType.MERGE: When the parent entity is merged (updated), the associated child entity will also be merged.
CascadeType.REMOVE: When the parent entity is removed (deleted), the associated child entity will also be removed.
CascadeType.REFRESH: When the parent entity is refreshed, the associated child entity will also be refreshed.
CascadeType.DETACH: When the parent entity is detached from the persistence context, the associated child entity will also be detached.

## OnetoOne

Mối quan hệ 1 - 1 giữa 2 bảng, 1 bản ghi của bảng này tương ứng 1 với bản ghi của bảng kia
user - profile

```sh
    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "profile_id")
    private Profile profile;
```

## ManytoOne : bảng phụ ( bảng ở giữa )

Mối quan hệ nhiều - 1, nhiều bản ghi ở bảng này ứng với 1 bản ghi của bảng kia, 1 - nhiều tương tự

```sh
  @ManyToOne
    @JoinColumn(name = "id_user", referencedColumnName = "id")
    private User user;

    @ManyToOne
    @JoinColumn(name = "id_course", referencedColumnName = "id")
    private Course course;
```

## ManytoMany : bảng chính ( 1 trong 2 bảng )

```sh
@ManyToMany
@JoinTable(
name = "student_course", // Tên bảng phụ
joinColumns = @JoinColumn(name = "student_id"), // Khoá ngoại trong bảng phụ, tham chiếu tới bảng Student
inverseJoinColumns = @JoinColumn(name = "course_id") // Khoá ngoại trong bảng phụ, tham chiếu tới bảng Course
)
private Set<Course> courses = new HashSet<>();
```
