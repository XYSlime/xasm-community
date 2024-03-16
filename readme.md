# XASM Community
参考UP主[乔然的计算机世界](https://space.bilibili.com/1285279188)的 XASM 制作的社区拓展版本的 XASM 。
[编译方法](./build.md)

## 1. 对比[原UP](https://space.bilibili.com/1285279188)的XASM_V1的特点

1. 开放了源代码，可以供大家学习和使用。

2. 跨平台支持，支持Windows、Linux、MacOS等操作系统。

3. 支持位运算指令。

## 2. 指令集

以下是XASM Community的指令，使用了[原UP](https://space.bilibili.com/1285279188)的XASM指令集并加上了位运算的指令。

### 2.1. 运算类

|指令|指令Hex|说明|调用格式|
|:-|:-|:-|:-|
|add|0x01|加法运算|add 被加数地址 加数地址|
|sub|0x02|减法运算|sub 被减数地址 减数地址|
|xadd|0x03|乘法运算|xadd 被乘数地址 乘数地址|
|xsub|0x04|除法运算|xsub 被除数地址 除数地址|

<!-- ```yml
add 指向被加数的地址 指向加数地址 # 执行1次加法运算 (hex: 0x01)

sub 指向被减数的地址 指向减数地址 # 执行1次减法运算 (hex: 0x02)

xadd 指向被乘数的例子 指向乘数地址 # 执行1次乘法运算 (hex: 0x03)

xsub 指向被除数的地址 指向除数地址 # 执行1次除法运算 (hex: 0x04)
``` -->

### 2.2. 逻辑判断类

|指令|指令Hex|说明|调用格式|
|:-|:-|:-|:-|
|and|0x11|逻辑与运算|and 地址1 地址2 存放布尔值的地址|
|or|0x12|逻辑或运算|or 地址1 地址2 存放布尔值的地址|
|not|0x13|逻辑非运算|not 地址1 存放布尔值的地址|

<!-- ```yml
and 地址1 地址2 存放布尔值的地址 # 进行一次与运算，返回为1表示成立，返回为0表示不成立 (hex: 0x11)

or 地址1 地址2 存放布尔值的地址 # 进行一次或运算，返回为1表示成立，返回为0表示不成立 (hex: 0x12)

not 地址1 地址2 存放布尔值的地址 # 进行一次非运算，返回为1表示成立，返回为0表示不成立 (hex: 0x13)
``` -->

### 2.3. 控制类

|指令|指令Hex|说明|调用格式|
|:-|:-|:-|:-|
|mov|0x21|把地址的值改成操作数|mov 地址 操作数|
|copy|0x22|复制地址2的值到地址1|copy 地址1 地址2|
|goto|0x23|跳转到地址指针指向的地址|goto 指向跳转地址的指针|
|geta|0x24|保存下一个指令的地址到指定地址|geta 地址|
|\>|0x25|大于判断，为真则跳转到指定位置|> 地址1 地址2 指向跳转位置的地址|
|<|0x26|小于判断，为真则跳转到指定位置|< 地址1 地址2 指向跳转位置的地址|
|=|0x27|等于判断，为真则跳转到指定位置|= 地址1 地址2 指向跳转位置的地址|
|lm|0x28|把地址往左移（不是<<）|lm 地址 把地址往左移动的次数的地址|
|rm|0x29|把地址往右移（不是>>）|rm 地址 把地址往右移动的次数的地址|
|exit|0x2a|退出|exit|
|sto|0xff|忽略其中的命令不执行，但会被编译出来|sto 数据 sto|


<!-- ```yml
mov 地址 操作数 # 执行1次赋值操作，此操作不需要直接寻址，填入地址和操作数即可 (hex: 0x21)

copy 地址1 地址2 # 复制地址2内的数据到地址1 (hex: 0x22)

goto 地址 # 从地址中读取输入并找到接下来要跳转的位置 (hex: 0x23)

geta 地址 # 获得当前程序计数器的位置并回存到指定地址 (hex: 0x24)

> 地址1 地址2 指向跳转位置的地址 # 执行1次大于判断，如果成立，跳转到地址指向的位置 (hex: 0x25)

< 地址1 地址2 指向跳转位置的地址 # 执行1次小于判断，如果成立，跳转到地址指向的位置 (hex: 0x26)

= 地址1 地址2 指向跳转位置的地址 # 执行1次相等判断，如果成立，跳转到地址指向的位置 (hex: 0x27)

lm 源地址 指向左移次数的地址 # (hex: 0x28)

rm 源地址 指向石移次数的地址 # (hex: 0x29)

exit # 结束程序的运行 (hex: 0x2a)
``` -->

### 2.4. 输入输出类

|指令|指令Hex|说明|调用格式|
|:-|:-|:-|:-|
|putc|0x31|输出一个字符|putc 指向字符地址的地址|
|putn|0x32|输出一个数字|putn 指向数字地址的地址|
|puth|0x33|输出一个16进制数|puth 指向16进制数地址的地址|
|getc|0x34|获取一个字符并保存到指定的地址|getc 字符存储的地址|
|getn|0x35|获取一个数字并保存到指定的地址|getn 数字存储的地址|
|geth|0x36|获取一个16进制数并保存到指定的地址|geth 16进制数存储的地址|

<!-- ```yml
putc 指向一个地址的指针 # 输出一个字符，从输入中获取对应的地址，然后从地址中获取要输出的内容 (hex: 0x31)

putn 指向一个地址的指针 # 输出一个数字，从输入中获取对应的地址，然后从地址中获取要输出的内容 (hex: 0x32)

puth 指向一个地址的指针 # 输出一个16进制数，从输入中获取对应的地址，然后从地址中获取要输出的内容 (hex: 0x33)

getc 地址 # 从键盘上获取一个字符并保存到指定的地址 (hex: 0x34)

getn 地址 # 从键盘上获取一个整型数据并保存到指定的地址 (hex: 0x35)

geth 地址 # 从键盘上获取一个整型数据并保存到指定的地址 (hex: 0x36)
``` -->

### 2.5. 位运算
|指令|指令Hex|说明|调用格式|
|:-|:-|:-|:-|
|&|0x41|地址1与地址2的值按位与，结果保存到地址1|& 地址1 地址2|
|\||0x42|地址1与地址2的值按位或，结果保存到地址1|\| 地址1 地址2|
|^|0x43|地址1与地址2的值按位异或，结果保存到地址1|^ 地址1 地址2|
|~|0x44|把地址中的值按位取反，结果保存到地址|~ 地址|
|<<|0x45|把数字左移后，保存到原来的地址|<< 数字的地址 左移次数的地址|
|\>>|0x46|把数字右移后，保存到原来的地址|>> 数字的地址 右移次数的地址|

以上就是关于XASM Community里的全部信息和指令了


## 3. XASM Compile Community 编译器

XASM Community还有自己的编译器，名字叫XASM Compile Community。（源码也在这个项目中公开）

### 3.1 主要用法

通过给编译后的程序传递 `--help` 参数获取帮助

### 3.2 特点

XASM Compile Community编译器有以下特点

1. 可以识别以 `//`、`#`、`--` 开头的注释，这意味着可以使代码可读性提高，编译成ROM文件后并不会保留注释。

2. 不加指令前缀也可以使用0xXX存储单个字节的数据

3. 可以使用字符串 `"要保留的内容"` 或者 `'要保留的内容'`  来在编译成ROM文件时保留一些认为必须要保留的内容，这样就可以在ROM文件中存储一些资源了，注意: 编译后的ROM文件并不会留下`"`或`'`符号。

4. 支持字符串中使用转义字符，现支持的有：
    - `\n` 换行
    - `\t` 制表符
    - `\\` 反斜杠
    - `\"` 双引号
    - `\'` 单引号

5. 仅支持使用0xXX 0xXX 0xXX 0xXX来存储操作数，编译成ROM文件后，会自动拼接指令后面分段存储的单字节数据并作为输入处理