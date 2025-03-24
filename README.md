 # ADVANCE C
 
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
- STDART là một thư viện có các hàm điển hình như printf và scanf
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

<details>
<summary>POINTER</summary>

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

**POINTER NULL**
- Con trỏ null là con trỏ không trỏ đến bất kì địa chỉ hợp lệ nào 
```c
int *ptr = NULL;
```
***Tại sao lại sử dụng con trỏ NULL?***
- Phòng tránh truy cập vùng nhớ rác :con trỏ chưa khởi tạo chứa giá trị ngẫu nhiên , giá trị ngẫu nhiên này vô tình trỏ đến vùng nhớ nguy hiểm 
- Kiểm tra : dễ dàng phát hiện con trỏ chưa được gán giá trị hợp lệ 
_ví dụ_
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
***Lưu ý : đối với con trỏ NULL không thể tham trị con trỏ NULL***

**POINTER TO POINTER**
_Tại sao cần đến con trỏ đến con trỏ?_
_Là khi bạn muốn thay đổi ĐỊA CHỈ mà một con trỏ đang trỏ đến từ bên trong con trỏ khác_
_ví dụ_
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

_ví dụ kinh điển:_
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

**CONST POINTER**
_Phân loại con trỏ hằng_

| Loại       | Thay đổi địa chỉ        | Thay đổi giá trị       | Khởi tạo bắt buộc |
|-------------|-------------|-------------|------|
| Con trỏ thường     |    :white_check_mark:| :white_check_mark:|:x:|
| Con trỏ hằng   |:white_check_mark:|:x:|:x:|
| Hằng con trỏ   | :x:  | :white_check_mark:  |:white_check_mark:|
|Hằng con trỏ đến hằng |:x:|:x:|:white_check_mark:|


**Con trỏ hằng**
_Mục đích:cho phép trỏ đến vùng nhớ nhưng KHÔNG thay đổi giá trị_
_cú pháp_
>const kieu_du_lieu *bien_con_tro;

```c
const int *ptr;
```
_ví dụ_
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
**Hằng con trỏ**
_Mục đích : cố định địa chỉ nhưng cho phép thay đổi giá trị_
>kieu_du_lieu *const bien_con tro =&ten_bien ;

***Lưu ý : phải khởi tạo ngay khi khai báo***

```c
int *const ptr=&near;
```
_ví dụ_
```c
int main(){
    int x=5 , y=10;
    int *const ptr =&x
    *ptr =7; // Hợp lệ : thay đổi được giá trị 
    ptr=&y; // Lỗi : không thể thay đổi giá trị 
    return 0;
}
```
**Hằng con trỏ đến hằng**
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
<summary>CONTROL FLOW VÀ XỬ LÝ LỖI</summary>

**CONTROL FLOW VÀ XỬ LÝ LỖI**
_Tổng quan về Control Flow_
Mặc định chương trình C thực hiện các câu lệnh từ trên xuống dưới .Như vậy , CPU làm từ hàm main , thực hiện lần lượt các câu lệnh và kết thúc tại điểm cuối hàm main
Tuy nhiên, trong thực tế , chúng ta cần các cơ chế :
- Thực thi một khối lệnh nhiều lần (vòng lặp : loops)
- Thực thi một khối lệnh chỉ khi thỏa mãn một điều kiện nào đó (branches)
- Nhảy đến 1 vị trí khác trong code (jumps)
- Xử lý tình huống lỗi và ngoại lệ (error handling)

**Câu lệnh goto**
_Là câu lệnh cho phép chương trình nhảy vô điều kiện đến 1 vị trí được đánh dấu bởi một nhãn_
_cú pháp_
>goto labell;
//các dòng code này sẽ được bỏ qua 
label : statement;

_ví dụ_
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
**Câu lệnh SETJMP và LONGJMP**
_Cơ chế hoạt động_
- SETJMP : lưu trữ trạng thái hiện tại vào biến jmb_buf
-LONGJMP : khôi phục trạng thái đã lưu , làm cho chương trình tiếp tục thực thi từ vị trí setjmp ban đầu 
```c
#include <setjmp.h>
jmp_buf env; // biến lưu trữ trạng thái 
int R =setjmp(env);// Lưu trữ trạng thái hiện tại 
void longjmp(jmp_buf env , int val); // khôi phục trạng thái 
```
_Lưu ý : setjmp : đánh dấu vị trí có thể quay lại bằng longjmp_
_Kết quả trả về lần đầu tiên bằng 0 , trả về 1 giá trị khác cho lần tiếp theo_
_Longjmp : nhảy về vị trí hiện tại khi thực hiện setjmp và tiếp tục_
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
**Xử lý ngoại lệ**
- Khối TRY : là phạm vi thực thi có khả năng sinh lỗi , không được sử dụng đơn độc mà phải đi kèm với catch , throw
- Khối THROW : tạo đối tượng ngoại lệ chứa thông tin debug
- Khối CATCH: Bẫy lỗi thông minh 
<details>
<summary>BÀI TẬP SỐ 2</summary>

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