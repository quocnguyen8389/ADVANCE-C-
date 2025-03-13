#COMPILER - PREPROCESS -MACRO
 -Quy trình biên dịch gồm :
     + Tiền xử lý : loại bỏ comment , xử lý include-define , tạo file.i(intermediate)
     +Biên dịch :chuyển file.i sang file.s(assembly) :gcc -S main.i -O main.s
     + Hợp ngữ :chuyển file.s sang file.o(mã máy): gcc -c main.s -O main.o
     + Liên kết : tạo file thực thi bằng cách kết hợp các file.o 
-The preprocess
     +INCLUDE
     +DEFINE
- Macro
  + ifdefine
  + ifndefine
  + endif
ví dụ 1: viết 1 chương trình sử dụng define định nghĩa hàm nhân 2 giá trị với nhau với a=5+1; và b=6;



