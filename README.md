 # COMPILER - PREPROCESS -MACRO
- Quy trình biên dịch :
_Tiền xử lý : loại bỏ các comment , xử lý include ,define , tạo file.i (intermediate)_
>gcc -E main.c -o main.i
    
 _Biên dịch : chuyển file.i sang file.s (assembly)_
>gcc -S main.i -O main.s.
    
 _Hợp ngữ :chuyển file.s sang file.o(mã máy)_
> gcc -c main.s -O main.o

_Liên kết : tạo file thực thi bằng cách kết hợp các file.o_
>gcc main.o -o main

- the preprocess
_include_
*define*
- Macro
 *ifdef*
 *ifndef*
 *endif*
 
*ví dụ 1 :ví dụ 1: viết 1 chương trình sử dụng define định nghĩa hàm nhân 2 giá trị với nhau với a=5+1; và b=6*
>#include<stdio.h>
#define mul(x,y) ((x)*(y))
int main()
{
     int a=5+1;
     int b=6;
     int KQ = mul(a,b)
     printf("kết quả nhân 2 giá trị :%d\n",KQ);
     return 0;
}

***Ý nghĩa :học cách sử dụng define và lưu ý khi sử dụng 2 giá trị thì tối ưu hóa chúng bằng dấu ngoặc đơn từng giá trị tránh việc ưu tiên toán tử làm sai kết quả***
*ví dụ: hãy viết 1 chương trình sử dụng #ifndef và giải thích tại sao sử dụng ?*

>#ifndef MY_HEADER_H  
#define MY_HEADER_H
#include <stdio.h>
void H(){
     printf("HELLO");
}
#endif

***ý nghĩa: học cách sử dụng ifndef : kiểm tra file.h đã được định nghĩa hay chưa ? nếu đã được định nghĩa thì không run đoạn chương trình phía dưới , nếu chưa định nghĩa thì run bình thường , phương pháp này có thể sử dụng để tránh trùng lặp hàm thư viện hoặc là việc định nghĩa file.h quá 1 lần***

## STDART - ASSERT
- Stdart là một thư viện có các hàm điển hình như printf và scanf
- cơ chế 
  _va_list_: **tạo biến** 
  _va_start_:**khởi tạo** liên kết với _va_list_ với tham số cố định :*ví dụ : va_start(ap ,format);*
  _va_arg_:**truy xuất tham số, phải chỉ định kiểu dữ liệu**
  _va_end_ : **dọn dẹp , giải phóng tài nguyên**

*ví dụ: viết hàm tính tổng cho số nguyên*
>#include <stdio.h>
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

-***Assert***:dùng để kiểm tra điều kiện phải xảy ra trong quá trình run , nếu đúng điều kiện thì chương trình tiếp tục run , nếu sai thì chương trình sẽ dừng lại 
_ví dụ:viết 1 chương trình sử dụng assert_
>#include<assert.h>
void chia(int a , int b){
     assert(b!=0); // vì b là mẫu nên phải khác 0
     printf("%d\n",a/b);
}

**lưu ý: nếu chúng ta bổ sung hàm "#define:NDEBUG" thì tất cả các assert sẽ bị tắt**

### BITMASK 
- bitmask là kĩ thuật sử dụng các biến riêng lẻ để biểu thị cho một trạng thái : 1 - bật , 0 - tắt
- Các phép toán bitmask 
 _set bit_: sử dụng toán tử OR
 _clear bit_: sử dụng toán tử đảo ~ và AND (lưu ý đảo xảy ra trước and)
 _toggle bit_ : sử dụng toán tử ^
 _check bit_: sử dụng toán tử AND "&"

 _ví dụ: Hãy xây dựng hệ thống quản lý quyền truy cập của người dùng bằng cách sử dụng kỹ thuật bitmask. Mỗi quyền sẽ được biểu diễn bằng một bit trong số nguyên. Hệ thống phải hỗ trợ các thao tác sau:**thêm quyền , xóa quyền , kiểm tra quyền , hiển thị quyền**_
_gợi ý : ta cần định nghĩa 4 quyền bằng một bit trong số nguyên thêm quyền ta sử dụng toán set bit , xóa quyền ta sử dụng clear bit , kiểm tra quyền ta sử dụng check bit và hiển thị quyền đã có thì ta dựa trên check bit và xuất ra quyền đã có ở check bit_
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

**BÀI TẬP: Phân tích mã nguồn sau (slide 14 HALA)**
>#include <stdio.h>
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

_định nghĩa màu , công suất , động cơ bằng define_
>typedef uint8_t CarColor;
typedef uint8_t CarPower;
typedef uint8_t CarEngine;

_sử dụng typedef uint8_t để định nghĩa các biến , nguyên nhân sử dụng typedef để dễ dàng thay đổi kiểu dữ liệu trong tương lai , nếu cần thay đổi kiểu dữ liệu uint8_t sang kiểu khác , chỉ cần sửa nơi định nghĩa typedef là được_


>#define SUNROOF_MASK 1 << 0     // 0001
#define PREMIUM_AUDIO_MASK 1 << 1 // 0010
#define SPORTS_PACKAGE_MASK 1 << 2 // 0100
// Thêm các bit masks khác tùy thuộc vào tùy chọn

_sử dụng Macro define để định nghĩa bit cho các biến_
>typedef struct {
    uint8_t additionalOptions : 3; // 3 bits cho các tùy chọn bổ sung
    CarColor color : 2;
    CarPower power : 2;
    CarEngine engine : 1;
    } CarOptions;

_mục đích sử dụng struct là tạo kiểu dữ liệu tùy chỉnh_
_carColor là lưu trữ màu với 2 bit ( phạm vi lưu trữ là 4 màu : 0-3(2^2-1)) đã được định nghĩa ở trên_
_carPower, carEngine cũng tương tự vậy_

>void configureCar(CarOptions *car, CarColor color, CarPower power, CarEngine engine, uint8_t options) {
    car->color = color;
    car->power = power;
    car->engine = engine;
    car->additionalOptions = options;
}

_hàm này để gán các giá trị màu , công suất, động cơ , gán các tùy chọn bổ sung_
_riêng đối với biến car thì sử dụng con trỏ để lấy giá trị gốc nếu có thay đổi thì thay đổi từ giá trị gốc chứ không phải giá trị sao chép_
>void setOption(CarOptions *car, uint8_t optionMask) {
    car->additionalOptions |= optionMask;
}

_sử dụng thêm chức năng bằng lệnh OR giống các phép toán trong bitmask_
>void unsetOption(CarOptions *car, uint8_t optionMask) {
    car->additionalOptions &= ~optionMask;
}

_sử dụng xóa chức năng bằng lệnh đảo ~ và AND trong bitmask_

>void displayCarOptions(const CarOptions car) {
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

_hàm này dùng để hiển thị những giá trị đã setup trước đó : màu , công suất , động cơ ... , có cả hiển thị thêm tùy chọn chức năng_
>int main() {
    CarOptions myCar;_
    configureCar(&myCar, COLOR_BLACK, POWER_150HP, ENGINE_2_0L, 0); 
	
 _đặt tên cho struct và cấu hình cho car theo các biến đã khai báo của hàm configureCar_


    setOption(&myCar, SUNROOF_MASK);
    setOption(&myCar, PREMIUM_AUDIO_MASK);
_ set thêm 2 chức năng là sunroof và audio_
>displayCarOptions(myCar);

_hiển thị chức năng đã set_
   >unsetOption(&myCar, PREMIUM_AUDIO_MASK); 
    displayCarOptions(myCar);

_clear chức năng audio vừa set và hiển thị_

    printf("size of my car: %d\n", sizeof(CarOptions));
_in ra kích cỡ của mycar dựa trên sizeof()_

    return 0;
}
