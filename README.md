 # ADVANCE C
 
### BÀI HỌC 
<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">COMPILER - PREPROCESSOR</summary>

 **<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Quy trình biên dịch**

_Tiền xử lý : loại bỏ các comment , xử lý include ,define , tạo file.i (intermediate)_
>gcc -E main.c -o main.i
    
 _Biên dịch : chuyển file.i sang file.s (assembly),phân tích cú pháp, kiểm tra lỗi_
>gcc -S main.i -O main.s.
    
 _Hợp ngữ :chuyển file.s sang file.o(mã máy)_
> gcc -c main.s -O main.o

_Liên kết : tạo file thực thi bằng cách kết hợp các file.o_
>gcc main.o -o main

- **<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">the preprocess** : chỉ thực hiện thay thế các macro chứ không thực hiện tính toán 
_include_
*define*
- Macro :
 *ifdef*
 *ifndef*
 *endif*
 
*<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ 1 :ví dụ 1: viết 1 chương trình sử dụng define định nghĩa hàm nhân 2 giá trị với nhau với a=5+1; và b=6*
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
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Comment.svg" 
     width="50" 
     height="25" 
     style="filter: invert(41%) sepia(67%) saturate(463%) hue-rotate(72deg) brightness(97%) contrast(94%);">Ý nghĩa :học cách sử dụng define và lưu ý khi sử dụng 2 giá trị thì tối ưu hóa chúng bằng dấu ngoặc đơn từng giá trị tránh việc ưu tiên toán tử làm sai kết quả***

*<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ: hãy viết 1 chương trình sử dụng #ifndef và giải thích tại sao sử dụng ?*
```c
#ifndef MY_HEADER_H  
#define MY_HEADER_H
#include <stdio.h>
void H(){
     printf("HELLO");
}
#endif
```
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Comment.svg" 
     width="50" 
     height="25" 
     style="filter: invert(41%) sepia(67%) saturate(463%) hue-rotate(72deg) brightness(97%) contrast(94%);">ý nghĩa: học cách sử dụng ifndef : kiểm tra file.h đã được định nghĩa hay chưa ? nếu đã được định nghĩa thì không run đoạn chương trình phía dưới , nếu chưa định nghĩa thì run bình thường , phương pháp này có thể sử dụng để tránh trùng lặp hàm thư viện hoặc là việc định nghĩa file.h quá 1 lần***

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Toán tử tiền xử lý**
- Toán tử tiếp tục "\\" : toán tử này cho phép bạn viết tiếp macro cho nhiều dòng 
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
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

***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">Câu hỏi :Sự khác biệt giữa #include <file.h> và #include "file.h" là gì ?***
_#include <file.h> chỉ định tiền xử lý tìm kiếm file trong thư mục include của hệ thống_
_#include "file.h" chỉ định tiền xử lý tìm kiếm trong file thư mục hiện tại trước, nếu không tìm thấy mới tìm trong hệ thống_

</details>


<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">STDART - ASSERT</summary>

 STDART - ASSERT
- STDART là một thư viện có các hàm điển hình như printf và scanf
 **<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">cơ chế** 

| tên hàm      | giải thích       
|-------------|-------------|
| va_list   | tạo biến   | 
| va_start   | khởi tạo liên kết với va_list với các tham số cố định : va_start(ap , format);   |
|va_arg|truy vấn tham số , phải chỉ định kiểu dữ liệu|
|va_end| dọn dẹp, giải phóng tài nguyên| 

*<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ: viết hàm tính tổng cho số nguyên*
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
-**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Assert**
- Dùng để kiểm tra điều kiện phải xảy ra trong quá trình run , nếu đúng điều kiện thì chương trình tiếp tục run , nếu sai thì chương trình sẽ :
  - In ra thông báo lỗi chi tiết (tên file , số dòng , biểu thức)
  - Gọi hàm abort() để KẾT THÚC chương trình 
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ:viết 1 chương trình sử dụng assert_
```c
#include<assert.h>
void chia(int a , int b){
     assert(b!=0); // vì b là mẫu nên phải khác 0
     printf("%d\n",a/b);
}
```
_**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Repository.svg" 
     width="50" 
     height="25" 
     style="filter: invert(12%) sepia(92%) saturate(6282%) hue-rotate(12deg) brightness(101%) contrast(117%);">Nguyên tắc vàng** để sử dụng assert: chỉ dùng để kiểm tra điều kiện tuyệt đối : tuyệt đối không bao giờ vi phạm hoặc tuyệt đối sẽ phải xuất hiện_
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Comment.svg" 
     width="50" 
     height="25" 
     style="filter: invert(41%) sepia(67%) saturate(463%) hue-rotate(72deg) brightness(97%) contrast(94%);">lưu ý: nếu chúng ta bổ sung hàm "#define:NDEBUG" thì tất cả các assert sẽ bị tắt , tuy nhiên phải define NDEBUG TRƯỚC khai báo thư viện _assert.h_**
</details>


<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">BITMASK </summary>
 BITMASK 
 **<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Bitwise operators**

 | Toán tử      | ý nghĩa       | ứng dụng       |
|-------------|-------------|-------------|
| &   | AND   | check bit và clear bit   |
|    | OR   | set bit   |
|~|NOT|toggle bit |
|<<|dịch trái   |nhân 2^n|
|>>|dịch phải |chia 2^n|

- bitmask là kĩ thuật sử dụng các biến riêng lẻ để biểu thị cho một trạng thái : 1 - bật , 0 - tắt
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Các phép toán bitmask** 

| PHÉP TOÁN      | PHƯƠNG HƯỚNG HOẠT ĐỘNG       | 
|-------------|-------------|
| set bit  | sử dụng toán tử OR  | 
| clear bit   |sử dụng toán tử đảo ~ và AND (lưu ý đảo xảy ra trước and)   | 
|toggle bit|sử dụng toán tử ^|
|check bit|sử dụng toán tử AND "&"|

_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ: Hãy xây dựng hệ thống quản lý quyền truy cập của người dùng bằng cách sử dụng kỹ thuật bitmask. Mỗi quyền sẽ được biểu diễn bằng một bit trong số nguyên. Hệ thống phải hỗ trợ các thao tác sau:**thêm quyền , xóa quyền , kiểm tra quyền , hiển thị quyền**_
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
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">KĨ THUẬT BITMASK ĐỘNG**
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
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ : hệ thống quản lý GPIO động_
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
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">BIT FIELDS**
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
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">Phân tích mã nguồn slide 14</summary>

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

<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">POINTER</summary>

 <img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);"> POINTER 
 - Con trỏ là một biến dùng để lưu địa chỉ của biến khác , nghĩa là biến thông thường chứa giá trị thì con trỏ chứa địa chỉ bộ nhớ (nơi mà giá trị được lưu trữ )  
 __Khai báo con trỏ__
 >kieu_du_lieu *ten_con_tro;
 
 *<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ :*
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
*<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ:*
```c
int number =4;
int *ptr =&number;
printf("giá trị của number=%d",number);
printf("địa chỉ của number=%d",&number);
printf("giá trị của ptr=%d",ptr); 
//giá trị của ptr là địa chỉ của number
printf("giá trị của con trỏ ptr(giá trị tại địa chỉ mà ptr trỏ đến)=%d",*ptr);
```
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Repository.svg" 
     width="50" 
     height="25" 
     style="filter: invert(12%) sepia(92%) saturate(6282%) hue-rotate(12deg) brightness(101%) contrast(117%);">Sau đây là bảng tổng kết nội dung**
| Đặc điểm      | Khai báo con trỏ       | Gán địa chỉ con trỏ       | Truy xuất con trỏ |
|-------------|-------------|-------------|--------|
| Cú pháp   | Kieu_du_lieu *Ten_con_tro   | Ten_con_tro =&Ten_bien   | *Ten_con_tro       |
| Mục đích  | Khai báo một biến đặc biệt có khả năng lưu trữ địa chỉ biến khác   | lập mối quan hệ : gán địa chỉ của 1 biến vào con trỏ     | Truy cập giá trị tại địa chỉ mà con trỏ đang trỏ đến        |
|Gía trị trả về | Không có | địa chỉ bộ nhớ | giá trị tại địa chỉ bộ nhớ 
 
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);"> Kích thước con trỏ**
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_:
```c
char *out;
float *put;
int *ar;
```
*<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">Câu hỏi :Kích thước các con trỏ trên có giống nhau không?*
>Tất cả các con trỏ đều có cùng 1 kích thước , KHÔNG PHỤ THUỘC VÀO KIỂU DỮ LIỆU MÀ CHÚNG TRỎ ĐẾN MÀ PHỤ THUỘC VÀO KIẾN TRÚC HỆ THỐNG (STM32, ESP32...)

*Nguyên nhân :con trỏ lưu trữ địa chỉ mà địa chỉ bộ nhớ trên 1 hệ thống có kích thước cố định (hệ thống 64 bit :8 byte ...)*
___Hiểu lầm : Nhiều người hiểu rằng (*int) lớn hơn (*char) .Điều này hoàn toàn sai : con trỏ lưu trữ địa chỉ nên kích thước của nó hoàn toàn không liên quan đến___
 
 **<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Con trỏ void**
 - Định nghĩa : void pointer là một loại con trỏ có thể trỏ đến dữ liệu của bất kì kiểu nào 
 _<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
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

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">FUNCTION POINTER**
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

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Comment.svg" 
     width="50" 
     height="25" 
     style="filter: invert(41%) sepia(67%) saturate(463%) hue-rotate(72deg) brightness(97%) contrast(94%);">CẢ HAI CÁCH ĐỀU CHO KẾT QUẢ GIỐNG NHAU**
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
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

***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Repository.svg" 
     width="50" 
     height="25" 
     style="filter: invert(12%) sepia(92%) saturate(6282%) hue-rotate(12deg) brightness(101%) contrast(117%);">Bảng tổng hợp con trỏ hàm***
| Khai báo con trỏ hàm     | Gán địa chỉ       | Gọi hàm thông qua con trỏ       |
|-------------|-------------|-------------|
|  kieu_tra_ve (*ten_con_tro)(ds_tham_so);  | con_tro =&ten_ham; hoặc contro =ten_ham ;   | (*con_tro_ham)(doi_so) hoặc (con_tro_ham)(doi_so)    |

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">POINTER NULL**
- Con trỏ null là con trỏ không trỏ đến bất kì địa chỉ hợp lệ nào 
```c
int *ptr = NULL;
```
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">Tại sao lại sử dụng con trỏ NULL?***
- Phòng tránh truy cập vùng nhớ rác :con trỏ chưa khởi tạo chứa giá trị ngẫu nhiên , giá trị ngẫu nhiên này vô tình trỏ đến vùng nhớ nguy hiểm 
- Kiểm tra : dễ dàng phát hiện con trỏ chưa được gán giá trị hợp lệ 
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
#include <stdio.h>
int main (){
    int *ptr =NULL; // khởi tạo 1 con trỏ NULL
    if(ptr=NULL){
        printf("con trỏ chưa được khởi tạo\n");
    }
    int giatri=3;
    ptr=&giatri;
    return 0;
}
```
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Comment.svg" 
     width="50" 
     height="25" 
     style="filter: invert(41%) sepia(67%) saturate(463%) hue-rotate(72deg) brightness(97%) contrast(94%);">Lưu ý : đối với con trỏ NULL không thể tham trị con trỏ NULL***

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">POINTER TO POINTER**
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">Tại sao cần đến con trỏ đến con trỏ?_
_Là khi bạn muốn thay đổi ĐỊA CHỈ mà một con trỏ đang trỏ đến từ bên trong con trỏ khác_
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
void change(int *ptr){
int value =20;
ptr=&value;   // giá trị ptr(địa chỉ biến a trong p) đang được gán là địa chỉ value
}
int main ()
{
    int a=10;
    int *p=&a;
    change(p);
    printf("%d",*p);//kết quả vẫn bằng 10
}
```
>value là biến toàn cục chỉ tồn tại trong phạm vi hàm => khi kết thúc hàm , địa chỉ value không còn hợp lệ 
>giải pháp : dùng con trỏ cấp 2 để thay đổi con trỏ gốc

**Khai báo**
```c
int **pptr;
```
_Minh họa_
_pptr có giá trị là địa chỉ của biến ptr_
_ptr có giá trị là địa chỉ biến value_
_value có giá trị là 20_
>nếu *pptr thì chỉ truy cập giá trị của biến ptr là địa chỉ biến value
nếu **pptr thì sẽ truy cập đến giá trị của value

_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ kinh điển:_
```c
#include <stdio.h>
void swap_pointer(int **a , int **b){
    //int **a(b) cho phép truy cập và sửa đổi địa chỉ mà ptr1 và ptr2 trỏ đến nghĩa là sửa đổi địa chỉ 0x1000 và 0x2000
    int *temp =*a;//a=&ptr1(giá trị của a là địa chỉ ptr1=0x3000), vậy *a =giá trị ptr1=0x1000(địa chỉ biến x)
    //temp=0x1000, vậy *temp =giá trị x =10;
    *a=*b;
    //b=&ptr2(0x4000) vậy *b=giá trị tại ptr2(0x2000)
    // a=0x2000; *a=20;
    *b=temp;//b=0x1000, vậy *b=10;
}
int main (){
    int x=10,y=20;
    int *ptr1=&x; // gán giá trị ptr1 là địa chỉ biến x
    //ví dụ: địa chỉ x =0x1000 , ptr1=0x1000 , địa chỉ ptr1=0x3000
    int *ptr2=&y; // gán giá trị ptr2 là địa chỉ biến y
    // ví dụ : địa chỉ y=0x2000 , ptr2=0x2000 , địa chỉ ptr2=0x4000
    printf("Trước swap:\n");
    printf("ptr1 → %d\n", *ptr1); // 10
    printf("ptr2 → %d\n", *ptr2); // 20
    swap_pointers(&ptr1, &ptr2);
    // truyền đại chỉ biến ptr1=0x3000, và ptr2=0x4000 
    // tại thời điểm này, không truyền giá trị của ptr1 và ptr2 vì chúng ta cần thay đổi địa chỉ 2 con trỏ 
    printf("Sau swap:\n");
    printf("ptr1 → %d\n", *ptr1); // 20
    printf("ptr2 → %d\n", *ptr2); // 10

    return 0;
}
```
| Bước       | code       | giải thích     |
|-------------|-------------|-------------|
| 1  | int *temp = *a;  | *a là giá trị tại 0x3000 (0x1000) → temp = 0x1000 (trỏ đến x)  |
| 2   | *a = *b;   | *b là giá trị tại 0x4000 (0x2000) → Gán *a = 0x2000 (ptr1 trỏ đến y)   |
|3|*b = temp;|temp = 0x1000 → Gán *b = 0x1000 (ptr2 trỏ đến x)|

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">CONST POINTER**
_Phân loại con trỏ hằng_

| Loại       | Thay đổi địa chỉ        | Thay đổi giá trị       | Khởi tạo bắt buộc |
|-------------|-------------|-------------|------|
| Con trỏ thường     |    :white_check_mark:| :white_check_mark:|:x:|
| Con trỏ hằng   |:white_check_mark:|:x:|:x:|
| Hằng con trỏ   | :x:  | :white_check_mark:  |:white_check_mark:|
|Hằng con trỏ đến hằng |:x:|:x:|:white_check_mark:|


**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Con trỏ hằng**
_Mục đích:cho phép trỏ đến vùng nhớ nhưng KHÔNG thay đổi giá trị_
_cú pháp_
>const kieu_du_lieu *bien_con_tro;

```c
const int *ptr;
```
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
int main(){
    int value =10;
    const int *ptr =&value;
    *ptr=30;// LỖI: không thể thay đổi được giá trị của ptr
    value =30;// Hợp lệ vì chúng ta thay đổi trực tiếp trên biến value không thông qua con trỏ
    ptr=&new;// Hợp lệ vì thay đổi địa chỉ 
}
```
_Bài học : dùng khi cần đảm bảo tính toàn vẹn của giá trị_
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Hằng con trỏ**
_Mục đích : cố định địa chỉ nhưng cho phép thay đổi giá trị_
>kieu_du_lieu *const bien_con tro =&ten_bien ;

***Lưu ý : phải khởi tạo ngay khi khai báo***

```c
int *const ptr=&near;
```
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
int main(){
    int x=5 , y=10;
    int *const ptr =&x
    *ptr =7; // Hợp lệ : thay đổi được giá trị 
    ptr=&y; // Lỗi : không thể thay đổi giá trị 
    return 0;
}
```
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Hằng con trỏ đến hằng**
_cú pháp_
>const kieu_du_lieu *const ten_con_tro =&ten_bien;

_Đặc điểm riêng: Không thay đổi được địa chỉ và cả giá trị_
**Kĩ thuật và thủ thuật**
_Quy tắc phân biệt_
__Đọc từ phải sang trái__
```c
const int *p1;
int const *p2;
int *const p3;
```
>int *p1 : con trỏ đến hằng (const)
const p3 hằng đến con trỏ (*p3)

> hằng là không đổi 
bên trái là địa chỉ - bên phải là giá trị // từ vỏ hộp(địa chỉ) vào trong hộp(giá trị) 
chữ hằng nằm bên nào thì bên đó không đổi , còn lại là đổi được 
</details>

<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">CONTROL FLOW VÀ XỬ LÝ LỖI</summary>

**CONTROL FLOW VÀ XỬ LÝ LỖI**
_Tổng quan về Control Flow_
Mặc định chương trình C thực hiện các câu lệnh từ trên xuống dưới .Như vậy , CPU làm từ hàm main , thực hiện lần lượt các câu lệnh và kết thúc tại điểm cuối hàm main
Tuy nhiên, trong thực tế , chúng ta cần các cơ chế :
- Thực thi một khối lệnh nhiều lần (vòng lặp : loops)
- Thực thi một khối lệnh chỉ khi thỏa mãn một điều kiện nào đó (branches)
- Nhảy đến 1 vị trí khác trong code (jumps)
- Xử lý tình huống lỗi và ngoại lệ (error handling)

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Câu lệnh goto**
_Là câu lệnh cho phép chương trình nhảy vô điều kiện đến 1 vị trí được đánh dấu bởi một nhãn_
_cú pháp_
>goto labell;
//các dòng code này sẽ được bỏ qua 
label : statement;

_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
#include <stdio.h>
int main (){
    int i=0;
    start_loop:
    printf("%d",i);
    i++;
    if(i<5)
    goto start_loop;
return 0;
}
```
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Câu lệnh SETJMP và LONGJMP**
_Cơ chế hoạt động_
- SETJMP : lưu trữ trạng thái hiện tại vào biến jmb_buf
-LONGJMP : khôi phục trạng thái đã lưu , làm cho chương trình tiếp tục thực thi từ vị trí setjmp ban đầu 
```c
#include <setjmp.h>
jmp_buf env; // biến lưu trữ trạng thái 
int R =setjmp(env);// Lưu trữ trạng thái hiện tại 
void longjmp(jmp_buf env , int val); // khôi phục trạng thái 
```
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Comment.svg" 
     width="50" 
     height="25" 
     style="filter: invert(41%) sepia(67%) saturate(463%) hue-rotate(72deg) brightness(97%) contrast(94%);">Lưu ý : setjmp : đánh dấu vị trí có thể quay lại bằng longjmp_
_Kết quả trả về lần đầu tiên bằng 0 , trả về 1 giá trị khác cho lần tiếp theo_
_Longjmp : nhảy về vị trí hiện tại khi thực hiện setjmp và tiếp tục_
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
#include <stdio.h>
#include <setjmp.h>
jmp_buf env;// biến lưu trạng thái 
void chia_so(int a, int b){
    if(b==0){
        printf("Phát hiện lỗi chia 0\n");
        longjmp(env,1); // nhảy đến vị trí setjmp với giá trị 1 
    }
    printf("KQ %d\n", a/b);
}
int main(){
    int error = setjmp(env);// lập chốt kiểm tra lỗi 
    if(error==0){
        printf("Thực hiện phép chia \n");
    }
    else
    printf("ĐÃ XẢY RA LỖI");
}
```
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Xử lý ngoại lệ**
- Khối TRY : là phạm vi thực thi có khả năng sinh lỗi , không được sử dụng đơn độc mà phải đi kèm với catch , throw
- Khối THROW : tạo đối tượng ngoại lệ chứa thông tin debug
- Khối CATCH: Bẫy lỗi thông minh 
<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">
BÀI TẬP SỐ 2</summary>

BÀI TẬP SỐ 2:
 Xử Lý Nhiều Loại Lỗi Trong Hệ Thống Phức Tạp Sử Dụng Macro TRY-CATCH
Mục Tiêu:
- Viết một chương trình trong ngôn ngữ C sử dụng các macro TRY, CATCH, và THROW để mô phỏng việc xử lý nhiều loại lỗi trong một hệ thống phức tạp.
Yêu Cầu:
- Định nghĩa các macro TRY, CATCH, và THROW giúp xử lý lỗi trong chương trình.
- Tạo các hàm giả lập các hoạt động khác nhau, mỗi hàm có khả năng "ném" ra một loại lỗi cụ thể sử dụng macro THROW.
- Trong hàm main, gọi các hàm này trong một khối TRY và xử lý các lỗi tương ứng trong các khối CATCH phù hợp.
- Các loại lỗi có thể bao gồm nhưng không giới hạn ở: lỗi đọc file, lỗi xử lý mạng, lỗi tính toán dữ liệu.
- In ra thông báo lỗi phù hợp khi một lỗi được bắt và xử lý.
Mô Tả Chi Tiết Hơn:
- Bạn cần viết ba hàm mô phỏng ba hoạt động khác nhau: readFile, networkOperation, và calculateData.
Mỗi hàm này sẽ sử dụng THROW để ném ra một loại lỗi cụ thể khi gặp sự cố.
- Trong main, sử dụng TRY để bao quanh việc gọi các hàm này và sử dụng các khối CATCH để xử lý từng loại lỗi riêng biệt.
Mỗi khối CATCH sẽ in ra một thông báo lỗi đặc trưng cho lỗi tương ứng.
- Đảm bảo chương trình kết thúc một cách an toàn, in ra thông báo kết thúc chương trình sau khi tất cả các lỗi đã được xử lý.
Cho một enum lưu các mã lỗi như sau: 
```C
enum ErrorCodes { NO_ERROR, FILE_ERROR, NETWORK_ERROR, CALCULATION_ERROR };
```
- Thông tin các hàm:
```c
void readFile() {
    printf("Đọc file...\n");
    THROW(FILE_ERROR, "Lỗi đọc file: File không tồn tại.");
}
void networkOperation() {
    // Bổ sung chương trình
}
void calculateData() {
   // Bổ sung chương trình
}
```
- Chương trình trong hàm main:
```c
TRY {
        readFile();
        networkOperation();
        calculateData();
    } CATCH(FILE_ERROR) {
        printf("%s\n", error_message);} // Bổ sung thêm nhiều CATCH
```
**GIẢI**
```C
#include<stdio.h>
#include<stdlid.h>
#include<setjmp.h>
enum ErrorCodes { 
    NO_ERROR, 
    FILE_ERROR, 
    NETWORK_ERROR, 
    CALCULATION_ERROR 
};// định nghĩa các mã lỗi 

typedef struct {
    int code; // mã lỗi
    const char* message; // thông báo lỗi 
}Error_Info;
jmp_buf env;// lưu trữ thông tin lỗi 
#define TRY if(Error_Info.code==0) // nếu setjmp=0 thực thi code trong TRY , và khác 0 nhảy đến CATCH
#define CATCH(error_code)\
else if(Error_Info.code == error_code)
#define THROW (code,message)\
Error_Info.code=code;\ // GÁN MÃ LỖI 
Error_Info.message=message;\ // GÁN THÔNG BÁO LỖI
longjmp(env,code)\ //
void readFile() {
    printf("Đang đọc file...\n");
    // Giả lập lỗi đọc file
    THROW(FILE_ERROR, "Lỗi đọc file: File không tồn tại hoặc bị khóa");
}

void networkOperation() {
    printf("Đang thực hiện kết nối mạng...\n");
    // Giả lập lỗi mạng
    THROW(NETWORK_ERROR, "Lỗi mạng: Không thể kết nối đến server");
}

void calculateData() {
    printf("Đang tính toán dữ liệu...\n");
    // Giả lập lỗi tính toán
    THROW(CALCULATION_ERROR, "Lỗi tính toán: Giá trị đầu vào không hợp lệ");
}
int main() {
Error_Info.code=setjmp(env);
    TRY {
        readFile();
        networkOperation();
        calculateData();
    }
    CATCH(FILE_ERROR) {
        fprintf(stderr, "[LỖI %d] %s\n", current_error.code, current_error.message);
    }
    CATCH(NETWORK_ERROR) {
        fprintf(stderr, "[LỖI %d] %s\n", current_error.code, current_error.message);
    }
    CATCH(CALCULATION_ERROR) {
        fprintf(stderr, "[LỖI %d] %s\n", current_error.code, current_error.message);
    }

    printf("\nKết thúc chương trình an toàn\n");
    return 0;
}
```
</details>

</details>
<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">STORAGE CLASSES</summary>


**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);"> EXTERN**

- Cho phép biến được KHAI BÁO Ở MỘT FILE nhưng có thể SỬ DỤNG Ở FILE KHÁC.Nó tạo ra tham chiếu đến biến tồn tại thay vì tạo ra một biến mới 
_Chú ý : Vì nó chỉ là một tham chiếu đến một biến đã được định nghĩa ở nơi khác nên KHÔNG CÓ BỘ NHỚ NÀO ĐƯỢC CẤP PHÁT_
_Liên kết các nội dung_
>gcc ten_file1.c ten_file2.c -o main 
nhập "./tenfile_canchay"
```C
//khai báo extern 
extern int bienToancuc;
//sử dụng biến extern 
void ham(){
    printf("%d",bienToancuc);
}
```
_Nguyên lý hoạt động:_
_Khi bạn làm việc với nhiều file.c trong dự án quá trình biên dịch sẽ diễn ra ở điểm quan trọng là : extern cho các trình liên kết biết rằng " biến này ở đâu đó trong các file , hãy tìm và liên kết "_
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
**fileA.c(định nghĩa biến)**
```c
int same=10;
```
**fileB.c(sử dụng biến từ fileA.c)**
```c
#include<stdio.h>
extern int same;// đây là biến toàn cục nên để ngoài hàm main
int main (){
    printf("biến extern :%d",same);
}
```
**Lưu ý quan trọng: không được khởi tạo giá trị cho biến khi khai báo với extern**
```c
extern int a; // đúng: khai báo extern không khởi tạo giá trị 
extern int a =300; // sai :khai báo extern đã vi phạm khởi tạo giá trị
```
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">Bài tập cá nhân***
- Tạo 3 file : math.h( khai báo extern PI 3.14) , circle.c (định nghĩa PI và hàm tính diện tích hình tròn) , main.c (sử dụng PI và hàm circle.c)
- Yêu cầu : sử dụng extern cho cả biến và hàm , in ra diện tích hình tròn và bán kính nhập từ bàn phím 
```c
//math.h 
extern const float PI  // thỏa mãn điều kiện extern không được khai báo và là biến toàn cục , đặt kiểu dữ liệu là float (số dư ) và const là hằng số q
extern float circleA(float r) // đáp ứng yêu cầu đề bài là extern cả hàm 

// circle.c
const float PI 3.14
float circleA(float r){
return PI*r*r;}

main.c
#include "math.h"
int main(){
    float ban_kinh;
    printf("nhập bán kính\n");
    scanf("%f",&ban_kinh);
    printf("Dientich:%.4f",circleA(ban_kinh));
    return 0;
}
```
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);"> STATIC**

- Là công cụ kiểm soạt phạm vi và thời gian tồn tại của biến và hàm 
- Nó hoạt động khác biệt giữa 2 ngữ cảnh : biến cục bộ trong hàm và biến/hàm toàn cục 
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">STATIC CHO BIẾN CỤC BỘ TRONG HÀM***
_ĐẶC ĐIỂM :_
_Khởi tạo một lần duy nhất khi chương trình bắt đầu(nếu chưa được khởi tạo sẽ tự gán giá trị bằng 0), giữ giá trị giữa các lần gọi hàm, chỉ có phạm vi trong hàm_
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ kinh điển_
```c
#include <stdio.h>
void count(){
    static int calls =0;// chỉ xảy ra 1 lần duy nhất
    printf("Số lần gọi ;%d\n",calls);
}
int main (){
    count();//1
    count();//2
    count();//3
    printf("Số lần gọi trong main :%d\n",calls);// lỗi biến calls chỉ giữ giá trị trong hàm count và trong hàm main biến calls cũng không được định nghĩa nên gây lỗi
    return 0;
}
```
_Nếu bỏ dòng:_
```c
printf("Số lần gọi trong main :%d\n",calls);
```
_Kết quả in ra là :_
>Số lần gọi: 1
Số lần gọi: 2
Số lần gọi: 3

_Nếu thay thế_
```c
static int calls =0
```
thay thế bằng 
```c
int calls =0;
```
_Kết quả_
>Số lần gọi: 1
Số lần gọi: 1
Số lần gọi: 1

***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">STATIC CHO BIẾN/HÀM TOÀN CỤC***
_Tính năng_
- giới hạn phạm vi trong file hiện tại 
- Ngăn xung đột tên 
- Thường được dùng với mẹo là ẩn biến /hàm khỏi các file khác , chỉ cho phép truy cập trong cùng 1 file 
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Bài tập cá nhân***
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">BÀI 1:Phân tích output chương trình sau_
```c
#include <stdio.h>

void test() {
    static int x ;
    x++;
    printf("%d ", x);
}

int main() {
    test(); // ?
    test(); // ?
    return 0;
}
```
_Kết quả_
>1 2

_Nguyên nhân biến x chưa được khởi tạo sẽ tự động gán giá trị là 0_
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">BÀI 2:Phân tích output chương trình sau_
```c
#include <stdio.h>

static int x = 5;

void test() {
    static int x = 10;
    x++;
    printf("%d", x);
}

int main() {
    test(); // ?
    test(); // ?
    printf("\nKết quả x=%d", x); // ?
    return 0;
}
```
_Kết quả_
>11 12  //static tồn tại trong hàm 
Kết quả x=5   // static tồn tại trong cả file

***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);"> VOLATILE***
- Được sử dụng để khai báo 1 biến có giá trị của nó có thể thay đổi bất kỳ lúc nào bởi yếu tố tác động bên ngoài 
- Ngăn trình biên dịch tối ưu hoặc xóa 1 biến đi
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
void wait(){
    uint8_t *status =(uint8_t*)0x2000000;

    while (*status==0){
        //thực hiện lệnh
    }
}
```

***Tuy nhiên trong code trên nếu không sử dụng volatide thì sẽ gặp tối ưu hóa vòng lặp nếu như quá trình lặp biến STATUS bằng 1 giá trị cố định quá nhiều lần***
```c
void wait(){
   volatile uint8_t *status =(uint8_t*)0x2000000;

    while (*status==0){
        //thực hiện lệnh
    }
}
```
***Việc sử dụng volatile sẽ giúp biến luôn thay đổi thay vì cố định giá trị khi bị cố định giá trị trong vòng lắp quá nhiều lần***

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">REGISTER**
- Là một gợi ý cho compiler lưu trữ biến trong CPU thay vì bộ nhớ RAM để tăng tốc độ truy cập
_cú pháp_
> register kieu_du_lieu ten_bien;

_Hạn chế : REGISTER không thể lấy được địa chỉ bằng toán tử & , và số lượng thanh ghi có hạn nên không thể đặt tất cả các biến vào register_
_ví dụ_
```c
void test(int arr[], int size){
    register int i=0;
    int sum=0;
    for(in i , i<size , i++){
        sum+=a[i];
    }
    return sum;
}
```
***Trong ví dụ trên , biến i được đề xuất lưu vào thanh ghi vì nó được truy cập thường xuyên trong vòng lặp***

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Repository.svg" 
     width="50" 
     height="25" 
     style="filter: invert(12%) sepia(92%) saturate(6282%) hue-rotate(12deg) brightness(101%) contrast(117%);">Kết luận**
- Extern cho phép truy cập biến/hàm từ các file khác , KHÔNG TẠO MỚI biến mà tham chiếu biến đã tồn tại trong các file (Không được khởi tạo khi khai báo)
- Static :biến toàn cục giới hạn phạm vi chỉ trong file hiện tại , biến cục bộ giữ giá trị giữa các lần gọi ham 
- Volatile giúp ngăn chặn các tối ưu hóa không mong muốn của compiler khi làm việc với biến có thể thay đổi từ bên ngoài 
- Register là GỢI Ý để tăng tốc độ truy cập 
</details>

<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">STRUCT - UNION</summary>

## KIỂU DỮ LIỆU TÙY CHỈNH 
 **<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">STRUCTS**
- Cấu trúc STRUCT cho phép đóng gói các kiểu dữ liệu khác nhau thành 1 thể duy nhất
- Mỗi thành phần trong STRUCT có một vùng nhớ riêng biệt 
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Quản lý bộ nhớ trong STRUCT***
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
struct B1{
     char a; //1 byte
     int b;  // 4 byte 
     char c;  //1 byte 
};
// bộ nhớ B1 được cấp phát là 4 byte 
// size = [1+ 3(padding)] + [4] + [1+3(padding)]=12 byte

struct B2{
     int a;//4 byte
     char a; //1 byte
     char c;  //1 byte 
};
// bộ nhớ B2 vẫn được cấp phát là 4 byte nhưng sẽ được tổ hợp khác 
// size = [4] + [1] + [1] +[2] =8 byte 
// 2 giá trị [1] và [1] được tổ hợp trong 4 byte tiếp theo sau 4 byte đầu
```
***Quy tắc vàng : sắp xếp thành phần theo thứ tự giảm dần kích thước để tối ưu hóa padding***
**Kĩ thuật #pragma pack**
_cú pháp_
>#pragma pack(push , n)  //lưu trạng thái hiện tại và đặt n byte mới 
#pragma pack(n)  // đặt alignment(n =1 ,2 ,4 ...)
#pragma pack(pop) // khôi phục trạng thái trước đó 
#pragma pack()  //reset về giá trị mặt định ( thường là 8)

_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
#pragma pack(push , 1) // không padding 
struct sensor {
     uint8_t head;// 1 byte và 3 padding 
     float arm;//4 byte
     uint16_t ear;//2 byte +2 padding
};
#pragma pack(pop) // khôi phục padding
// size =1+4+2=7
//giảm từ 12 xuống 7
```
_Nhờ có việc sử dụng #pragma pack nên đã loại bỏ các byte padding_ 
***Nhược điểm là sẽ gây nguy hiểm khi làm việc với DMA : DMA yêu cầu alignment chính xác theo phần cứng , việc thay đổi packing có thể dẫn đến lỗi hệ thống***

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">UNION**
- Là kiểu dữ liệu cho phép các thành phần **chia sẻ cùng vùng nhớ**
_Đặc điểm_
- Tất cả các thành phần dùng chung 1 vùng nhớ
- Kích thước UNION = thành phần lớn nhất 
- Chỉ một thành phần có giá trị hợp lệ ở một thời điểm
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Repository.svg" 
     width="50" 
     height="25" 
     style="filter: invert(12%) sepia(92%) saturate(6282%) hue-rotate(12deg) brightness(101%) contrast(117%);">So sánh UNION và STRUCT***

| STRUCT        | UNION       |
|-------------|-------------|
| Mỗi thành phần có 1 vùng nhớ riêng    | Tất cả dùng chung vùng nhớ   | 
| Kích thước lớn hơn hoặc bằng tổng thành phần    | Kích thước bằng thành phần lớn nhất    
|Truy cập đồng thời được |Chỉ 1 thành phần tại 1 thời điểm|

_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
struct R {
     int a ;
     char b;
}; // size =8

union R {
     int a;
     char b ;
}; // size =4
```
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">Câu hỏi ôn tập kiến thức_
1. Tại sao kích thước struct thường lớn hơn tổng kích thước các thành phần?
- Nguyên nhân do **HIỆU ỨNG CĂN CHỈNH BỘ NHỚ** và **CƠ CHẾ PADDING TỰ ĐỘNG**
- Khi compiler xử lý struct , nó sẽ thêm các byte padding giữa các thành phần để đảm bảo hiệu ứng căn chỉnh 
> công thức : kích thước struct = tổng kích thước thành phần + tổng padding
2. Vì sao đôi khi union hữu ích hơn struct trong lập trình nhúng?
Dưới đây là các nguyên nhân :
- ưu thế trong việc tiết kiệm bộ nhớ dứa trên cơ chế chia sẻ vùng nhớ
- Linh hoạt trong việc truy xuất dữ liệu
 kỹ thuật type punning cho phép truy cập cùng một vùng nhớ dưới nhiều kiểu dữ liệu khác nhau mà không cần chuyển đổi tường minh 
 ```c
 union Converter{
     uint32_t packet; //4bytes
     struct {
          uint8_t byte1; // LSB 
          uint8_t byte2;
          uint8_t byte3;
          uint8_t byte4;//MSB
     }bytes;
 };
 ```
 > cùng vùng nhớ packet và bytes chia sẻ chung 4 bytes bộ nhớ 

 với việc đặt giá trị 0xA1B2C3D4
 | Địa chỉ       | giá trị hex     | thành phần       |
|-------------|-------------|-------------|
| 0x0000   | D4   | byte 1-LSB BYTE THẤP NHẤT  |
| 0x0001   | C3   | byte 2  |
|0x0002|B2|byte 3|
|0x0003|A1|byte 4 - MSB BYTE CAO NHẤT|

 Truy xuất
```c
union Converter conv
conv.packet = 0xA1B2C3D4;
printf("byte1: 0x%X\n",conv.bytes.byte1); //0xD4
printf("byte4: 0x%X\n",conv.bytes.byte4); //0xA1
```
3. Khi nào nên sử dụng union thay vì struct?
- Khi làm việc với bộ nhớ hạn chế 
- Khi cần tối ưu hiệu suất đường truyền
- Khi cần xử lý dữ liệu đa dạng không đồng thời ( int , char ...)
</details>

<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">MEMORY LAYOUT</summary>
 MEMORY LAYOUT
<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">TEXT SEGMENT

- Là nơi chứa mã máy được phiên dịch từ mã nguồn .Đây là vùng nhớ quyết định cách chương trình vận hành và tương tác với phần cứng 
_Đặc điểm_
- Tính chỉ đọc (read-only)
- Khả năng chia sẻ
- Vị trí địa chỉ thấp
_Thành phần nội dung_
- Mã máy đã biên dịch : chứa toàn bộ chỉ thị thực thi dưới dạng nhị phân
- Hằng số chương trình 
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">INITIALIZED DATA SEGMENT**
- Là nơi lưu trữ các biến toàn cục và biến tĩnh đã được khởi tạo với giá trị cụ thể khác 0
*ĐẶC ĐIỂM*
- Tính đọc - ghi 
- Phân loại :vùng chỉ đọc( chứa các hằng số const và chuỗi kí tự hằng) và vùng đọc ghi( chứa biến toàn cục , static có thể thay đổi giá trị)
- Vị trí cao hơn text segment nhưng thấp hơn BSS trong không gian bộ nhớ ảo 
*Lưu ý : các giá trị tự data segment được đọc từ file thực thi khi chương trình nạp vào bộ nhớ .Kích thước phân vùng này được xác định bởi kích thước của các biến trong mã nguồn và không thay đổi trong thời gian chạy*
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">Uninitialized data segment**
- Còn được gọi là BSS segment(Block started by symbol) là nơi lưu trữ các biến toàn cục và biến tĩnh chưa khởi tạo hoặc khởi tạo với giá trị bằng 0
*Đặc điểm*
- Khởi tạo giá trị 0
- Tiết kiệm không gian 
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
int gloman ;// biến toàn cục không khởi tạo được lưu trữ trong BSS
int main(){
     static int i;// biến tĩnh không khởi tạo được lưu trong BSS
     return 0;
}
```
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">STACK**
- Là vùng nhớ tự động 
_Đặc điểm_
- Cấp phát nhanh
- Tự động giải phóng 
- Biến cục bộ 
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">Ví dụ_
```c
void D{
     int x=5; // biến x lưu trong stack
}
```
***Stack frame***
Mỗi hàm tạo bởi stack frame chứa :
- Tham số hàm
- Địa chỉ trả về 
- Biến cục bộ 
- Gía trị thanh ghi cần bảo tồn
**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">HEAP**
_Đặc điểm nổi bật_
Heap là bộ nhớ động :
- Kích thước linh hoạt
- Truy cập qua con trỏ 
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
int *arr= malloc(1000000 * sizeof(int));// cấp phát 4mb trên heap
free(arr); // giải phóng thủ công
```
***Quy trình quản lý heap***
- malloc// calloc : cấp phát
- realloc : thay đổi kích thước
- free : giải phóng
_Lưu ý : bổ sung thư viên stdlid.h_

sử dụng hàm malloc()
```c
int size =5;
uint16_t *ptr =(uint16_t*)malloc(size * sizeof(uint16_t));
// tại sao sử dụng con trỏ ? vì cấp phát địa chỉ mà thao tác trên địa chỉ thì sử dụng con trỏ
//kết quả trả về là con trỏ void nên cần được ép kiểu để đúng với các giá trị hiển thị 
//Không khởi tạo giá trị , vùng nhớ sẽ chứa giá trị rác 
```
- Nên kiểm tra đã cấp phát giá trị hay chưa 
```c
if(ptr==NULL){
     printf("cấp phát thất bại ");
}
```
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Repository.svg" 
     width="50" 
     height="25" 
     style="filter: invert(12%) sepia(92%) saturate(6282%) hue-rotate(12deg) brightness(101%) contrast(117%);">Bảng so sánh_
| Tiêu chí       | Stack        | Heap      |
|-------------|-------------|-------------|
| Tốc độ   | Cực nhanh   | Chậm   |
| Quản lý   | Tự động    | Thủ công   |
|Truy cập |Biến cục bộ |Qua con trỏ |

***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">Bài tập được giao: tìm hiểu về sự khác biệt giữa calloc và malloc , realloc***
Khi nào nên sử dụng :
- MALLOC() :cần cấp phát nhanh , ghi đè toàn bộ dữ liệu ngay sau cấp phát , không quan tâm đến giá trị ban đầu 
- CALLOC() :cần đcảm bảo tất cả các giá trị ban đầu đều là 0 , làm việc với dữ liệu nhạy cảm , cần an toàn hơn khi truy cập dữ liệu 
- REALLOC() :cần thay đổi kích thước vùng nhớ đã cấp phát , muốn giữ nguyên dữ liệu hiện có khi thay đổi kích thước

_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Repository.svg" 
     width="50" 
     height="25" 
     style="filter: invert(12%) sepia(92%) saturate(6282%) hue-rotate(12deg) brightness(101%) contrast(117%);">So sánh chi tiết_

| Tiêu chí       | Malloc()       | Calloc()       | realloc()|
|-------------|-------------|-------------|-----|
| Mục đích  | cấp phát vùng nhớ động mới   | Cấp phát và khởi tạo vùng nhớ mới   | thay đổi kích thước vùng nhớ đã cấp phát|
| Khởi tạo giá trị    | Không(chứa giá trị rác )   | Có (tất cả đều là 0)   | giữ giá trị cũ và phần mới chứa biến rác|
An toàn|ít an toàn |an toàn hơn do khởi tạo |cần xử lý trường hợp trả về NULL|

***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Discussions.svg" 
     width="50" 
     height="25" 
     style="filter: invert(20%) sepia(80%) saturate(500%) hue-rotate(30deg) brightness(80%) contrast(60%);">Bài tập được giao 2: Những lưu ý quan trọng trong việc sử dụng cấp phát động***
- Luôn kiểm tra NULL sau khi cấp phát :
```c
int *p =(int*)malloc(size);
if(p== NULL){
     //XỬ LÝ LỖI
}
```
- Luôn giải phóng bộ nhớ khi không cần sử dụng 
```c
free(p);
p=NULL; //GÁN NULL để tránh lỗi dangling pointer
```
- Cẩn thận với Realloc():
```C
int * temp =(int*)realloc(p,new_size);
if(temp!=NULL){
     p=temp;
}else{
     //xử lý lỗi , giữ nguyên p
}
```
</details>

<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">LINKED LIST</summary>

**<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">LINKED LIST**
- Là cấu trúc dữ liệu bao gồm các nút (node) liên kết với nhau thông qua các liên kết (link)
- Mỗi nút chứa 2 thành phần : dữ liệu và con trỏ trỏ đến nút tiếp theo của chuỗi
- Đặc biệt , danh sách liên kết cấp phát bộ nhớ động trong quá trình chạy chương trình 
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
typedef struct Node{
     int data; // dữ liệu nút
    struct Node* next; // con trỏ đến nút kế tiếp 
}
```
> chúng ta cần con trỏ head để lưu vị trí nút đầu tiên

```c
Node* head =NULL;
```
***Các thao tác cơ bản***
- Thêm nút : có 2 vị trí cơ bản để thêm nút mới
-- Thêm vào đầu danh sách
_ví dụ minh họa_
```c
void insert (Node** head, int data){
     Node* newNode =(Node*)malloc(sizeof(Node));
     if(newNode == NULL){
     printf("Lỗi cấp phát bộ nhớ");
     return;
     }
     // gán dữ liệu 
     newNode->data= data;
     newNode->next = *head;
     // cập nhật head
     *head= newNode;
}
```
-- Thêm vào cuối danh sách
```c
void insert (Node** head, int data){
     Node* newNode =(Node*)malloc(sizeof(Node));
     if(newNode == NULL){
     printf("Lỗi cấp phát bộ nhớ");
     return;
     }
     // gán dữ liệu 
     newNode->data= data;
     newNode->next = NULL;
     // Nếu danh sách rỗng
     if(*head == NULL){
          *head = newNode;
          return;
     }
     // tìm nút cuối cùng 
     Node* last = *head;
     while(last->new!= NULL){
          last= last->new;
     }
     //liên kết nút cuối với nút mới 
     last->new = newNode;
}
```
-- Xóa nút 
```c
void deleteNode(Node** head , int key){
     Node* temp =* heap;
     Node* prev = NULL;
     //Nếu nút cần xóa là head
     if(temp != NULL && temp->data == key){
          *head =temp->next;
          free(temp);
          return;
     }
     // tìm nút cần xóa
     while(temp!= NULL && temp->data != key){
          prev=temp;
          temp= temp->next;
     }
     // nếu không tìm thấy key 
     if(temp == NULL )
     return;
    // ngắt liên kết và giải phóng bộ nhớ
    prev->next= temp->next;
    free(temp);
}
```
-- Duyệt danh sách
```c
void Display(Node* head){
     Node* current=head;
     while(current!= NULL){
          printf("%d", current->data);
          current=current->next;
     }
     printf("NULL");
}
```
***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">TRICK***
- Ngoài việc sử dụng void thì sẽ được lưu trên stack thì chúng ta có thể sử dụng con trỏ để được lưu trên heap 
_ví dụ_
```c
// sử dụng void
void create_note(Node *node , int newData){
     node->next = NULL;
     node->data =newData;
}
// sử dụng con trỏ 
Node* create_note(int newData){
     Node *node =(Node*)malloc(sizeof(Node));
     node->next = NULL;
     node->data =newData;
     return node;
}
```
</details>

<details>
<summary><img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Release.svg" width="50" height="25">STACK - QUEUE</summary>

**STACK**
- Hoạt động theo nguyên tắc Last In First Out (LIFO): vào sau ra trước (hình ảnh trực quan là chồng đĩa , nơi có thể thêm hoặc lấy đĩa từ đỉnh )
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Comment.svg" 
     width="50" 
     height="25" 
     style="filter: invert(41%) sepia(67%) saturate(463%) hue-rotate(72deg) brightness(97%) contrast(94%);">Đặc điểm_
- Tuân thủ quy tắc LIFO : vào sau ra trước 
- Chỉ cho phép truy cập phần tử ở đỉnh 
- Triển khai tất cả thao tác đều thực hiện trên đỉnh
_Các thao tác cơ bản_
1. **Push** : thêm phần tử ở đỉnh 
2. **Pop** :lấy và xóa phần tử ở đỉnh
3. **Peek/Top** : xem giá trị phần tử ở đỉnh mà không xóa 
4. **isEmpty**: kiểm tra ngăn xếp có rỗng không 
5. **isFull** : kiểm tra ngăn xếp có đầy chưa 

_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Comment.svg" 
     width="50" 
     height="25" 
     style="filter: invert(41%) sepia(67%) saturate(463%) hue-rotate(72deg) brightness(97%) contrast(94%);">Như vậy_
- **push -> top++** : tăng thêm thì giá trị bổ sung 
- **pop -> top--** : giảm đi thì giá trị phải trừ ra
- **top =-1 -> stack rỗng**
- **top =size - 1 -> stack đầy**

_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ triển khai bằng mảng_
```c
typedef struct{
     int *items;// mảng lưu phần tử 
     int size ; // số lượng phần tử 
     int top; // thể hiện giá trị đỉnh ở ngăn xếp
}Stack;
// khởi tạo giá trị 
void stack_init(Stack *stack, int newSize ){
     stack->items=(int*)malloc(newSize *sizeof(int));// cấp phát động ra vùng nhớ 
     stack->size = newSize; // số lượng phần tử = newSize
     stack->top = -1;// stack rỗng 
}
// kiểm tra rỗng 
bool isEmpty(Stack stack){
     return (stack.top == -1 ? true : false);
}
// kiểm tra stack đầy 
bool isFull(Stack stack){
     return (stack.top == (stack.size-1) ? true : false);
}
// thêm phần tử 
void Push(Stack *stack , int data){
     if(isFull(*stack)){ // kiểm tra đã đầy chưa
          printf("full element\n");
     }
     else{
          stack-> top++;// bổ sung vùng để thêm phần tử 
          stack -> items[stack->top]=data;// ghi dữ liệu
     }
}
// xóa phần tử 
void Pop(Stack *stack , int data){
     if(isEmpty(*stack)){ // kiểm tra đã đầy chưa
          printf("empty element\n");
     }
     else{
          int value = stack ->items[stack->top];// đọc giá trị hiện tại đỉnh
          printf("giá trị top đỉnh=%d",value);
          stack->items[stack->top]=0;// ghi đè giá trị xóa bằng 0
          stack->top--;// xóa vùng cần đã ghi đè
     }
}
// đọc giá trị đỉnh
void Pop(Stack *stack , int data){
     if(isEmpty(*stack)){ // kiểm tra đã đầy chưa
          printf("empty element\n");
     }
     else{
          
          return stack->items[stack->top];
     }
}
// giải phóng bộ nhớ 
void free(Stack *stack){
     if(stack->items != NULL){
          free(stack->item);
          stack->items==NULL;
     }
}
```
**QUEUE**
- Hàng đợi là một cấu trúc dữ liệu tuyến tính được sử dụng lưu trữ và thao tác dữ liệu theo thứ tự 
- Hoạt động theo nguyên tắc FIFO(First In First Out) : nghĩa là phần từ đầu tiên được đưa vào sẽ là phần từ đầu tiên được lấy ra
- Một hàng đợi có hai đầu : đầu vào (rear) nơi các phần tử được thêm vào và đầu ra (front) nơi các phần tử lấy ra . 
***ĐIỂM QUAN TRỌNG*** :hàng đợi mở cả 2 đầu , khác với stack chỉ mở 1 đầu 
_Các thao tác cơ bản của hàng đợi_
1. **isEmpty()** : kiểm tra xem hàng đợi có rỗng hay không 
2. **isFull()** : kiểm tra xem hàng đợi có đầy hay không 
3. **enqueue()** : thêm 1 phần tử ở cuối hàng đợi
4. **dequeue()** : xóa 1 phần tử ở đầu hàng đợi
5. **peek()** :xem phần tử ở hàng đợi đầu mà không xóa nó
6. **initialize()** : khởi tạo 1 hàng đợi rỗng 
_Các triển khai hàng đợi_: thường sử dụng 2 con trỏ
1. **Front** : con trỏ đến phần tử đầu tiên hàng đợi
2. **Rear** : con trỏ đến phần tử cuối cùng ở hàng đợi
_Khi khởi tạo cả FRONT và REAR thường được đặt giá trị là -1 để biểu thị hàng đợi rỗng_

*Khi tăng phần tử*
> enqueue -> rear++
rear =size -1 -> queue full

*Khi giảm phần tử*
>dequeue -> front++
front == -1 hoặc front > rear hoặc front = rear + n ->queue empty

<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);"> Linear queue : 

-- Nếu REAR đạt tới giá trị max thì được coi là đầy và không thể thêm phần tử mới , ngay cả khi phía trước còn khoảng trống do các phần tử đã bị xóa 
-- Chỉ có thể thêm phần tử mới khi đã dequeue toàn bộ các phần tử hiện có ( queue rỗng hoàn toàn và front set về vị trí ban đầu)
```c
typedef struct {
     int *items;
     int size;
     int front;
     int rear;
}Queue;
//khởi tạo thông số ban đầu 
void queue_init(Queue *queue , int newSize){
     queue->items = (int*)malloc( newSize * sizeof(int));
     queue->size = newSize ;
     queue->front = queue->rear = -1; // khởi tạo giá trị chỉ rằng hàng đợi đang rỗng
}
//kiểm tra hàng đợi rỗng 
bool queue_isEmpty(Queue queue){
     return (queue.front == -1 || queue.front > queue.rear)?true:false;
     // tại đây có 2 điều kiện để xác định rỗng là front == -1 và trường hợp hàng đợi đã có phần tử nhưng bị xóa tất cả thể hiện front > rear
     // (khi xóa front tăng lên 1 , sau khi xóa đến phần tử cuối cùng thì front = n , trong khi rear = n-1 . do đó front > rear )
}
// kiểm tra hàng đợi đầy 
bool queue_isFull(Queue queue){
     return (queue.rear == queue.size -1 )?true: false;
}
//thêm phần tử vào hàng đợi 
void enqueue (Queue *queue , int value){
     if(queue_isFull(*queue)){
          printf("hàng đợi đầy\n");
     }
     else{
          if(queue->front == -1){
               queue->front == queue->rear=0;
               // khi thêm giá trị đầu tiên thì front và rear từ -1 sẽ tăng lên 0 
               // các trường hợp sau tăng thêm phần tử chỉ tăng rear 
               // vậy nên cần ktra có rỗng hay không để xác định có phải là thêm phần tử đầu tiên hay không
          }
          else{
               queue->rear++;
          }
          queue->items[queue->rear]= value;// tại vị trí trên ghi giá trị mới vào 
     }
}
// xóa phần tử ở cuối đợi
int dequeue(Queue queue){
     if(queue_isEmpty(*queue)){
          printf("hàng đợi rỗng\n");
     }
     else{
          // lưu vào 1 biến tạm
          int dequeue_value = queue->items[queue->front];
          // set giá trị cần xóa về 0
          queue->items[queue->front]=0;
          if(queue->front == queue->rear && queue->rear == queue->size -1){
               // theo điều kiện front = rear khi hàng đợi rỗng và hàng đợi chỉ còn 1 phần tử duy nhất 
               // điều kiện rear = size -1 , xét đến phần tử cuối của mảng 
               //nếu không sét về -1 thì front khi tăng sẽ lên 1 phần tử nằm ngoài mảng 
               queue->front = queue->rear =-1;
          }
          else{
               queue->front++;
               // tăng front cho đến khi front = rear
          }
          return dequeue_value;
     }
}
// đọc giá trị đầu hàng đợi
int front(Queue queue){
     if(queue_isEmpty(queue)){
          printf("Hàng đợi rỗng\n");
          return -1;
     }
     return queue.items[queue.front];
}
// đọc giá trị cuối hàng đợi
int rear(Queue queue){
      if(queue_isEmpty(queue)){
          printf("Hàng đợi rỗng\n");
          return -1;
     }
     return queue.items[queue.rear];
}
// giải phóng bộ nhớ 
int queue_free(Queue *queue){
     if(queue->items != NULL){
          free(queue->items);
          queue->items = NULL;
     }
}
```
 <img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Wiki.svg" 
     width="50" 
     height="25" 
     style="filter: invert(24%) sepia(73%) saturate(1446%) hue-rotate(212deg) brightness(98%) contrast(94%);">CIRCULAR QUEUE
- ***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Repository.svg" 
     width="50" 
     height="25" 
     style="filter: invert(12%) sepia(92%) saturate(6282%) hue-rotate(12deg) brightness(101%) contrast(117%);">Điểm mấu chốt*** : circular queue giải quyết triệt để vấn đề lãng phí bộ nhớ trong Linear queue bằng cách cho phép rear và front "quay vòng" khi đạt đến cuối mảng 
_Khác biệt cốt lõi giữa Linear queue và Circular queue_
_<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_
```c
bool queue_isFull(Queue queue){
     return (queue.rear= queue.size -1)? true : false;
}
```
 Nhược điểm chính :khi REAR đạt giá trị max_size dù FRONT đã được giải phóng không thể tái sử dụng vùng nhớ trống phía trước
 _<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/RequestedChanges.svg" 
     width="50" 
     height="25" 
     style="filter: invert(76%) sepia(87%) saturate(461%) hue-rotate(139deg) brightness(104%) contrast(97%);">ví dụ_: với queue_size =5;
 > ban đầu [A] [B] [C] [D] [E] (front =0 , rear =5-1=4)
 sau khi dequeue 2 lần : front = 2, rear =4;
 khoảng trống index 0 -1 không thể sử dụng 

 **<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Comment.svg" 
     width="50" 
     height="25" 
     style="filter: invert(41%) sepia(67%) saturate(463%) hue-rotate(72deg) brightness(97%) contrast(94%);">Kỹ thuật**: sử dụng phép modulo(%) tạo hiệu ứng vòng
 ```c
 queue->rear =(queue->rear + 1) % queue->size;
 queue->front =(queue->front + 1) % queue->size;
 ```
 > cho phép rear/front nhảy về 0 khi đạt giá trị max

 ***<img src="https://cdn.jsdelivr.net/gh/Readme-Workflows/Readme-Icons@main/icons/octicons/Repository.svg" 
     width="50" 
     height="25" 
     style="filter: invert(12%) sepia(92%) saturate(6282%) hue-rotate(12deg) brightness(101%) contrast(117%);">Cải tiến***
 1. Hàm kiểm tra đầy 
 ```c
 bool queue_isFull(Queue queue){
     if(queue.front ==-1)
     return false;
return ((queue.rear + 1) % queue.size) == queue.front;
 }
 ```
 2. Hàm thêm phần tử 
 ```c
 void enqueue(Queue *queue , int value){
     if(queue_isFull(*queue)){
          printf("hàng đợi rỗng \n");
          return;
     }
     if(queue->front == -1){
          queue->front == queue->rear ==0;
     }
     else{
          queue->rear= (queue->rear + 1) % queue->size;
     }
     queue->items[queue->rear]= value;
 }
 ```
 3. Hàm xóa phần tử 
 ```c
 int dequeue(Queue *queue ){
 if(queue_isEmpty(*queue)){
     printf("hàng đợi rỗng\n");
     return -1;
    }
    int dequeue_value =queue->items[queue->front];
    if(queue->front == queue->rear){
     queue->front = queue->rear = -1;
    }
    else{
     queue->front = (queue->front + 1) % queue->size; 
    }
    return dequeue_value;
 }
 ```
 </details>

 # MAKEFILE