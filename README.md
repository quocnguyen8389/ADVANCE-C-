 # ADVANCE C

### Thời gian cập nhật  
🔄 **Last Updated:** 2025-03-21 22:30:00 UTC

### BÀI HỌC 
<details>
<summary>COMPILER - PREPROCESSOR</summary>

- Quy trình biên dịch :

_Tiền xử lý : loại bỏ các comment , xử lý include ,define , tạo file.i (intermediate)_
>gcc -E main.c -o main.i
    
 _Biên dịch : chuyển file.i sang file.s (assembly),phân tích cú pháp, kiểm tra lỗi_
>gcc -S main.i -O main.s.
    
 _Hợp ngữ :chuyển file.s sang file.o(mã máy)_
> gcc -c main.s -O main.o

_Liên kết : tạo file thực thi bằng cách kết hợp các file.o_
>gcc main.o -o main

- **the preprocess** : chỉ thực hiện thay thế các macro chứ không thực hiện tính toán 
_include_
*define*
- Macro :
 *ifdef*
 *ifndef*
 *endif*
 
*ví dụ 1 :ví dụ 1: viết 1 chương trình sử dụng define định nghĩa hàm nhân 2 giá trị với nhau với a=5+1; và b=6*
```c
#include<stdio.h>
#define mul(x,y) ((x)*(y))
int main()
{
     int a=5+1;
     int b=6;
     int KQ = mul(a,b)
     printf("kết quả nhân 2 giá trị :%d\n",KQ);
     return 0;
}
```
***Ý nghĩa :học cách sử dụng define và lưu ý khi sử dụng 2 giá trị thì tối ưu hóa chúng bằng dấu ngoặc đơn từng giá trị tránh việc ưu tiên toán tử làm sai kết quả***

*ví dụ: hãy viết 1 chương trình sử dụng #ifndef và giải thích tại sao sử dụng ?*
```c
#ifndef MY_HEADER_H  
#define MY_HEADER_H
#include <stdio.h>
void H(){
     printf("HELLO");
}
#endif
```
***ý nghĩa: học cách sử dụng ifndef : kiểm tra file.h đã được định nghĩa hay chưa ? nếu đã được định nghĩa thì không run đoạn chương trình phía dưới , nếu chưa định nghĩa thì run bình thường , phương pháp này có thể sử dụng để tránh trùng lặp hàm thư viện hoặc là việc định nghĩa file.h quá 1 lần***

**Toán tử tiền xử lý**
- Toán tử tiếp tục "\\" : toán tử này cho phép bạn viết tiếp macro cho nhiều dòng 
_ví dụ_
```c
#define macro_R(a , b)\
printf("giá trị a=%d",a);\
printf("chia 2 giá trị=%f",a/b);\
while(0)\
```
- Toán tử stringize "#":toán tử này cho phép chuyển đổi các tham số thành chuỗi 
_ví dụ_
```c
#define in(x) printf(#x "= %d",x); // #x đã chuyển thành chuỗi dù nằm ngoài nháy kép
int a =6;
in(a);
```
>kết quả : a=6

- Toán tử token pasting "##" : toán tử nối 2 token lại với nhau 
_ví dụ_
```c
#define ME (X,Y) X##Y

int ME (HELLO,WORD) =5;
```
>KẾT QUẢ : HELLOWORD =5;

***Câu hỏi :Sự khác biệt giữa #include <file.h> và #include "file.h" là gì ?***
_#include <file.h> chỉ định tiền xử lý tìm kiếm file trong thư mục include của hệ thống_
_#include "file.h" chỉ định tiền xử lý tìm kiếm trong file thư mục hiện tại trước, nếu không tìm thấy mới tìm trong hệ thống_

</details>


<details>
<summary>STDART - ASSERT</summary>

 STDART - ASSERT
- Stdart là một thư viện có các hàm điển hình như printf và scanf
- cơ chế 

| tên hàm      | giải thích       
|-------------|-------------|
| va_list   | tạo biến   | 
| va_start   | khởi tạo liên kết với va_list với các tham số cố định : va_start(ap , format);   |
|va_arg|truy vấn tham số , phải chỉ định kiểu dữ liệu|
|va_end| dọn dẹp, giải phóng tài nguyên| 

*ví dụ: viết hàm tính tổng cho số nguyên*
```c
#include<stdio.h>
#include<stdarg.h>
int tong(int dem,...){
     int total=0;
     va_list ap;
     va_start (ap,dem);
     for( int i=0;i<=dem;i++){
          total+=va_arg(ap,int);
     }
     va_end(ap);
     return total;
}
int main(){
     printf("tổng các số sau %d\n",tong(5,6,4));
     return 0;
}
```
-***Assert***:dùng để kiểm tra điều kiện phải xảy ra trong quá trình run , nếu đúng điều kiện thì chương trình tiếp tục run , nếu sai thì chương trình sẽ :
  - In ra thông báo lỗi chi tiết (tên file , số dòng , biểu thức)
  - Gọi hàm abort() để KẾT THÚC chương trình 
_ví dụ:viết 1 chương trình sử dụng assert_
```c
#include<assert.h>
void chia(int a , int b){
     assert(b!=0); // vì b là mẫu nên phải khác 0
     printf("%d\n",a/b);
}
```
_**Nguyên tắc vàng** để sử dụng assert: chỉ dùng để kiểm tra điều kiện tuyệt đối : tuyệt đối không bao giờ vi phạm hoặc tuyệt đối sẽ phải xuất hiện_
**lưu ý: nếu chúng ta bổ sung hàm "#define:NDEBUG" thì tất cả các assert sẽ bị tắt , tuy nhiên phải define NDEBUG TRƯỚC khai báo thư viện _assert.h_**
</details>


<details>
<summary>BITMASK</summary>
 BITMASK 
 - Bitwise operators

 | Toán tử      | ý nghĩa       | ứng dụng       |
|-------------|-------------|-------------|
| &   | AND   | check bit và clear bit   |
|    | OR   | set bit   |
|~|NOT|toggle bit |
|<<|dịch trái   |nhân 2^n|
|>>|dịch phải |chia 2^n|

- bitmask là kĩ thuật sử dụng các biến riêng lẻ để biểu thị cho một trạng thái : 1 - bật , 0 - tắt
- Các phép toán bitmask 

| PHÉP TOÁN      | PHƯƠNG HƯỚNG HOẠT ĐỘNG       | 
|-------------|-------------|
| set bit  | sử dụng toán tử OR  | 
| clear bit   |sử dụng toán tử đảo ~ và AND (lưu ý đảo xảy ra trước and)   | 
|toggle bit|sử dụng toán tử ^|
|check bit|sử dụng toán tử AND "&"|

_ví dụ: Hãy xây dựng hệ thống quản lý quyền truy cập của người dùng bằng cách sử dụng kỹ thuật bitmask. Mỗi quyền sẽ được biểu diễn bằng một bit trong số nguyên. Hệ thống phải hỗ trợ các thao tác sau:**thêm quyền , xóa quyền , kiểm tra quyền , hiển thị quyền**_
_gợi ý : ta cần định nghĩa 4 quyền bằng một bit trong số nguyên thêm quyền ta sử dụng toán set bit , xóa quyền ta sử dụng clear bit , kiểm tra quyền ta sử dụng check bit và hiển thị quyền đã có thì ta dựa trên check bit và xuất ra quyền đã có ở check bit_
```c
>#include <stdio.h>
#include <stdint.h>
#define READ  (1 << 0)
#define WRITE  (1 << 1)
#define SPEAK  (1 << 2)
#define LISTEN  (1 << 3)
 void add_per(uint32_t *per,uint32_t perm){
     *per |=perm;
 }
void clear_per(uint32_t *per,uint32_t perm){
     *per &=~perm;
 }
void check_per(uint32_t *per,uint32_t perm){
     return (per &perm)=perm;
 }
void display_per(uint32_t per);{
     printf("Quyền hiện có ");
     if(check_per(per, READ)) printf("READ");
     if(check_per(per, WRITE)) printf("WRITE");
     if(check_per(per, SPEAK)) printf("SPEAK");
     if(check_per(per, LISTEN)) printf("LISTEN");
     printf("\n");
}
int main(){
     uint32_t user_permission=0;
     add_per(&user_permission,READ | SPEAK);
     display_per(user_permission);
     clear_per(&user_permission, SPEAK)
     display_per(user_permission);
}
```
**KĨ THUẬT BITMASK ĐỘNG**
- Bitmask động cho phép tạo mặt nạ bit theo vị trí linh hoạt bất kì .Đây là kĩ thuật THUỘC LÒNG
```c
#define BIT_MASK(start ,end) ((~0U<< (start))&(~0U>>(31-(end))))
```
>"~0U" : tạo 32 bit toàn là 1 (0xFFFFFFFF)
"<< (start)" : xóa các bit từ 0- start -1
 ">>(31 -end)" : xóa các bit từ end+1 đến 31
AND 2 kết quả : giữ lại bit từ start đến end

_ví dụ_
```c
BIT_MASK(2,4);
//kết quả sẽ bằng :0b011100 giữ lại số 1 tại vị trí từ 2-4
```
_ví dụ : hệ thống quản lý GPIO động_
_YÊU CẦU : điều khiển 32 GPIO , SET CLEAR nhiều chân cùng lúc , toggle dải chân bất kì_
```c
typedef struct {
    volatile uint32_t *port ;
} GPIO_typeDef;
void gpio_set(GPIO_typeDef *gpio, int start , int end){
    uint32_t mask = BIT_MASK(start ,end)
    *gpio->port |=mask;
}
```
**BIT FIELDS**
- Là 1 kĩ thuật giúp tiết kiêm bộ nhớ 
_cú pháp_
```c
struct hall{
    int tem :5;
    float hum :3;
}
```
>tổng là 8 bit thay vì nếu không khai báo số lượng bit thì sẽ là 16 bit chia đều cho 2 biến 

<details>
<summary>Phân tích mã nguồn slide 14</summary>

**BÀI TẬP: Phân tích mã nguồn sau (slide 14 HALA)**
```c
#include <stdio.h>
#include <stdint.h>
#define COLOR_RED 0	
#define COLOR_BLUE 1
#define COLOR_BLACK 2
#define COLOR_WHITE 3
#define POWER_100HP 0
#define POWER_150HP 1
#define POWER_200HP 2
#define ENGINE_1_5L 0
#define ENGINE_2_0L 1
```
_định nghĩa màu , công suất , động cơ bằng define_
```c
typedef uint8_t CarColor;
typedef uint8_t CarPower;
typedef uint8_t CarEngine;
```
_sử dụng typedef uint8_t để định nghĩa các biến , nguyên nhân sử dụng typedef để dễ dàng thay đổi kiểu dữ liệu trong tương lai , nếu cần thay đổi kiểu dữ liệu uint8_t sang kiểu khác , chỉ cần sửa nơi định nghĩa typedef là được_

```c
#define SUNROOF_MASK 1 << 0     // 0001
#define PREMIUM_AUDIO_MASK 1 << 1 // 0010
#define SPORTS_PACKAGE_MASK 1 << 2 // 0100
// Thêm các bit masks khác tùy thuộc vào tùy chọn
```
_sử dụng Macro define để định nghĩa bit cho các biến_
```c
typedef struct {
    uint8_t additionalOptions : 3; // 3 bits cho các tùy chọn bổ sung
    CarColor color : 2;
    CarPower power : 2;
    CarEngine engine : 1;
    } CarOptions;
```
_mục đích sử dụng struct là tạo kiểu dữ liệu tùy chỉnh_
_carColor là lưu trữ màu với 2 bit ( phạm vi lưu trữ là 4 màu : 0-3(2^2-1)) đã được định nghĩa ở trên_
_carPower, carEngine cũng tương tự vậy_
```c
void configureCar(CarOptions *car, CarColor color, CarPower power, CarEngine engine, uint8_t options) {
    car->color = color;
    car->power = power;
    car->engine = engine;
    car->additionalOptions = options;
}
```
_hàm này để gán các giá trị màu , công suất, động cơ , gán các tùy chọn bổ sung_
_riêng đối với biến car thì sử dụng con trỏ để lấy giá trị gốc nếu có thay đổi thì thay đổi từ giá trị gốc chứ không phải giá trị sao chép_
```c
void setOption(CarOptions *car, uint8_t optionMask) {
    car->additionalOptions |= optionMask;
}
```
_sử dụng thêm chức năng bằng lệnh OR giống các phép toán trong bitmask_
```c
void unsetOption(CarOptions *car, uint8_t optionMask) {
    car->additionalOptions &= ~optionMask;
}
```
_sử dụng xóa chức năng bằng lệnh đảo ~ và AND trong bitmask_
```c
void displayCarOptions(const CarOptions car) {
    const char *colors[] = {"Red", "Blue", "Black", "White"};
    const char *powers[] = {"100HP", "150HP", "200HP"};
    const char *engines[] = {"1.5L", "2.0L"};

    printf("Car Configuration: \n");
    printf("Color: %s\n", colors[car.color]);
    printf("Power: %s\n", powers[car.power]);
    printf("Engine: %s\n", engines[car.engine]);
    printf("Sunroof: %s\n", (car.additionalOptions & SUNROOF_MASK) ? "Yes" : "No");
    printf("Premium Audio: %s\n", (car.additionalOptions & PREMIUM_AUDIO_MASK) ? "Yes" : "No");
    printf("Sports Package: %s\n", (car.additionalOptions & SPORTS_PACKAGE_MASK) ? "Yes" : "No");}
```
_hàm này dùng để hiển thị những giá trị đã setup trước đó : màu , công suất , động cơ ... , có cả hiển thị thêm tùy chọn chức năng_
```c
int main() {
    CarOptions myCar;_
    configureCar(&myCar, COLOR_BLACK, POWER_150HP, ENGINE_2_0L, 0); 
```	
 _đặt tên cho struct và cấu hình cho car theo các biến đã khai báo của hàm configureCar_

```c
    setOption(&myCar, SUNROOF_MASK);
    setOption(&myCar, PREMIUM_AUDIO_MASK);
_ set thêm 2 chức năng là sunroof và audio_
>displayCarOptions(myCar);
```
_hiển thị chức năng đã set_
```c
   unsetOption(&myCar, PREMIUM_AUDIO_MASK); 
    displayCarOptions(myCar);
```
_clear chức năng audio vừa set và hiển thị_
```c
    printf("size of my car: %d\n", sizeof(CarOptions));
```
_in ra kích cỡ của mycar dựa trên sizeof()_
```c
    return 0;
}
```
</details>

</details>



 POINTER 
 - Con trỏ là một biến dùng để lưu địa chỉ của biến khác , nghĩa là biến thông thường chứa giá trị thì con trỏ chứa địa chỉ bộ nhớ (nơi mà giá trị được lưu trữ )  
 __Khai báo con trỏ__
 >kieu_du_lieu *ten_con_tro;
 
 *ví dụ :*
 ```c
 int *ptr;
 int *a;
 ```
 **Kiểu dữ liệu con trỏ cũng thể hiện kiểu dữ liệu mà biến nó trỏ đến theo nguyên tắc đồng kiểu dữ liệu**

 **Gán địa chỉ cho con trỏ**
 - Mỗi biến đều có 1 giá trị và 1 địa chỉ , để truy cập địa chỉ biến trong C ta sử dụng toán tử ***&***
 _ví dụ:_
 ```c
 int so =5;
 int *contro;
 contro = & so;
 ```
 >bây giờ kết quả là biến _contro_ đang nắm giữ địa chỉ của biến _so_

 **Truy xuất giá trị thông qua con trỏ**
- Khác với truy cập địa chỉ con trỏ sử dụng toán tử __&__ thì truy xuất giá trị sử dụng toán tử __*__ (được gọi là tham trị).
 __*__ ***:toán tử này truy xuất giá trị của địa chỉ mà con trỏ đang trỏ đến*** 
*ví dụ:*
```c
int number =4;
int *ptr =&number;
printf("giá trị của number=%d",number);
printf("địa chỉ của number=%d",&number);
printf("giá trị của ptr=%d",ptr); 
//giá trị của ptr là địa chỉ của number
printf("giá trị của con trỏ ptr(giá trị tại địa chỉ mà ptr trỏ đến)=%d",*ptr);
```
**Sau đây là bảng tổng kết nội dung**
| Đặc điểm      | Khai báo con trỏ       | Gán địa chỉ con trỏ       | Truy xuất con trỏ |
|-------------|-------------|-------------|--------|
| Cú pháp   | Kieu_du_lieu *Ten_con_tro   | Ten_con_tro =&Ten_bien   | *Ten_con_tro       |
| Mục đích  | Khai báo một biến đặc biệt có khả năng lưu trữ địa chỉ biến khác   | lập mối quan hệ : gán địa chỉ của 1 biến vào con trỏ     | Truy cập giá trị tại địa chỉ mà con trỏ đang trỏ đến        |
|Gía trị trả về | Không có | địa chỉ bộ nhớ | giá trị tại địa chỉ bộ nhớ 
 
**Kích thước con trỏ**
_ví dụ_:
```c
char *out;
float *put;
int *ar;
```
*Câu hỏi :Kích thước các con trỏ trên có giống nhau không?*
>Tất cả các con trỏ đều có cùng 1 kích thước , KHÔNG PHỤ THUỘC VÀO KIỂU DỮ LIỆU MÀ CHÚNG TRỎ ĐẾN MÀ PHỤ THUỘC VÀO KIẾN TRÚC HỆ THỐNG (STM32, ESP32...)

*Nguyên nhân :con trỏ lưu trữ địa chỉ mà địa chỉ bộ nhớ trên 1 hệ thống có kích thước cố định (hệ thống 64 bit :8 byte ...)*
___Hiểu lầm : Nhiều người hiểu rằng (*int) lớn hơn (*char) .Điều này hoàn toàn sai : con trỏ lưu trữ địa chỉ nên kích thước của nó hoàn toàn không liên quan đến___
 
 **Con trỏ void**
 - Định nghĩa : void pointer là một loại con trỏ có thể trỏ đến dữ liệu của bất kì kiểu nào 
 _ví dụ_
 ```c
 void *ptr;
 ```
> Con trỏ void không liên kết bất kì kiểu dữ liệu cụ thể nào , do đó nó có thể giữ địa chỉ của bất kì kiểu dữ liệu nào 
 
_ví dụ_
```c
#include<stdio.h>
int main(){
    int a=10;
    float b=11;
    void *ptr;// khai báo con trỏ void 
    // sử dụng con trỏ void trỏ đến kiểu int 
    ptr =&a;
    printf("Địa chỉ biến a :%p\n",ptr);
    // sử dụng con trỏ đến kiểu float
    ptr = &b;
     printf("Địa chỉ biến a :%p\n",ptr);
}
```
__Hạn chế của void pointer__
- Con trỏ void không thể truy cập trự tiếp giải tham chiếu bằng toán tử * (Nguyên nhân trình biên dịch không biết phải đọc bao nhiêu byte để thực hiện giải tham chiếu )
- Để truy cập giá trị , phải ép kiểu 
```c
void *ptr =&a;
int value =*(int*)ptr; 
// chúng ta phải ép kiểu (int*) , sử dụng tham chiếu * =*(int*)
```
***Sử dụng con trỏ void khi cần viết 1 hàm hoặc 1 cấu trúc có thể sẽ làm việc với nhiều kiểu dữ liệu , lưu ý luôn ghi nhớ kiểu dữ liệu gốc***

**FUNCTION POINTER**
- Mỗi hàm đều sẽ tồn tại trong bộ nhớ tại một địa chỉ nhất định 
- Con trỏ hàm (Function pointer) là một biến đặc biệt dùng để lưu trữ địa chỉ của một hàm
__cú pháp và cách khai báo__
>kieu_tra_ve (*ten_con_tro)(ds_tham_so);

**chú ý : dấu ngoặc đơn (*ten_con_tro) là bắt buộc**
```c
int (*ptr)(int , int);
void (*gtr)(char*);
```
__Gán địa chỉ cho hàm__
- Sau khi khai báo chúng ta cần gán địa chỉ : có 2 cách gán địa chỉ
>cách 1:con_tro =&ten_ham;
>cách 2:contro =ten_ham ;

**CẢ HAI CÁCH ĐỀU CHO KẾT QUẢ GIỐNG NHAU**
_ví dụ_
```c
#include <stdio.h>
int sub (int a , int b){
    return a-b;
}
int main (){
    int (*op)(int int);
    op=&sub;
    printf("kết quả %d\n ",op(4,3));// đáp án =1
    op=sub;
    printf("kết quả %d\n ",op(4,3));// đáp án =1
}
```
**Gọi hàm thông qua con trỏ hàm**
>(*con_tro_ham)(doi_so): cách 1
(con_tro_ham)(doi_so) : cách 2

***Bảng tổng hợp con trỏ hàm***
| Khai báo con trỏ hàm     | Gán địa chỉ       | Gọi hàm thông qua con trỏ       |
|-------------|-------------|-------------|
|  kieu_tra_ve (*ten_con_tro)(ds_tham_so);  | con_tro =&ten_ham; hoặc contro =ten_ham ;   | (*con_tro_ham)(doi_so) hoặc (con_tro_ham)(doi_so)    |



</details>

