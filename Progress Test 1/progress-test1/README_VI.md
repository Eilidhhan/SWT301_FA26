# SWT301 -- Progress Test 1

## Unit Testing với JUnit 5

### Kết quả chạy Test

Toàn bộ bộ test đã được chạy thành công trước và sau khi thực hiện
Manual Mutation Testing.

-   Số lượt test chạy: **185**
-   Failures: **0**
-   Errors: **0**
-   Skipped: **0**
-   Kết quả cuối cùng: **BUILD SUCCESS**

## Độ bao phủ kiểm thử -- JaCoCo Coverage

JaCoCo được sử dụng để đo độ bao phủ của các bài kiểm thử.

-   Instruction Coverage: **96%**
-   Branch Coverage: **93%**
-   Yêu cầu: Line Coverage \>= 80%, Branch Coverage \>= 70%
-   Kết quả: **Đạt**

Báo cáo JaCoCo được tạo tại:

`target/site/jacoco/index.html`

## Manual Mutation Testing

Ba lỗi giả lập (mutation) được tạo lần lượt trong mã nguồn. Sau mỗi lần
thay đổi, toàn bộ test được chạy lại để kiểm tra xem bộ test có phát
hiện được lỗi hay không. Sau khi ghi nhận kết quả, mã nguồn được hoàn
tác về trạng thái đúng.

  --------------------------------------------------------------------------------------------------------------
  Mutation          Lỗi được tạo               Các test phát hiện lỗi                          Đã hoàn tác
  ----------------- -------------------------- ----------------------------------------------- -----------------
  M1                Đổi                        `login_CorrectPasswordAfterNFailures`,          Có
                    `>= MAX_FAILED_ATTEMPTS`   `login_WhileLocked_RejectsWithoutIncrement`,    
                    thành                      `login_WrongPassword5thTime_LocksAccount`       
                    `> MAX_FAILED_ATTEMPTS`                                                    

  M2                Bỏ qua kiểm tra            `login_WhileLocked_RejectsWithoutIncrement`,    Có
                    `account.isLocked()` trong `login_CorrectPasswordAfterNFailures`           
                    `login()`                                                                  

  M3                Đổi giới hạn regex         `isValidUsername_InvalidValues_ReturnsFalse`,   Có
                    username từ `{4,19}` thành `isValidUsername_BoundaryLength`                
                    `{4,20}`                                                                   
  --------------------------------------------------------------------------------------------------------------

### Kết quả Mutation Testing

Cả **3 mutation** đều được các unit test hiện có phát hiện. Điều này cho
thấy các test đã kiểm tra được những lỗi quan trọng liên quan đến giới
hạn số lần đăng nhập sai, trạng thái khóa tài khoản và giá trị biên của
username.

Sau mỗi lần thử mutation, mã nguồn đều được sửa lại về trạng thái ban
đầu. Lần chạy test cuối cùng cho kết quả:

-   **185 tests**
-   **0 failures**
-   **0 errors**
-   **0 skipped**
-   **BUILD SUCCESS**

## Cách chạy chương trình kiểm thử

Chạy toàn bộ test:

``` bash
mvn clean test
```

Chạy riêng `AccountValidatorTest`:

``` bash
mvn -Dtest=AccountValidatorTest test
```

Chạy riêng `AccountServiceTest`:

``` bash
mvn -Dtest=AccountServiceTest test
```

Sau khi chạy test, mở báo cáo JaCoCo tại:

``` text
target/site/jacoco/index.html
```
