# 符合类型

## 数组

1. `short months[12];`
2. `int yam[3] = {33, 3, 5s};`
   * 如果只对一部分初始化，自动把其他初始化为0
3. `short things[] = {1, 4, 6, 7};`

## 字符串

1. c style string
   * `char dog[8] = {'b', 'e', 'a', 'u', '\0'};`
   * `char bird[] = "Bubbles";`
2. 读取字符串
   * `char name[size];`
   * `cin >> name;`: 遇到空白结束输入
3. 每次读取一行输入
   * `cin.getline()`: 读取一行，丢弃行尾换行
   * `cin.get()`: 读取一行，把换行放在输入队列
     * `cin.get()`: 可以读取下一个字符
     * `cin.get(name, arSize).get()`

## string类

* cpp 98标准添加了string类库拓展了c++库， 因此可以使用string类型的变量
  * string可以使用c风格字符串初始化
  * 可以使用cin, cout
  * 也可以使用数组表示法
* 赋值，拼接，附加
  * 可以将一个string赋值给另一个string
  * 可以使用运算符`+=`追加
  * 获取长度: `size()`
* 读取一行数据
  * `gitline(cin, str)`

## 其他形式的字符串字面值

1. 长字符类型

   * `wchar_t title[] = L"Chief";`
   * `char16_t name[] = u"Felonia`
   * `char32_t car[] = U"ieoje`

2. utf-8字符串常量

   * `string s = u8"龙龙"`

3. 原始字符串

   ```cpp
   cout << R"(jim \n ""  )"
   ```

## 结构简介

1. 基本结构语法

   ```cpp
   struct inflatable {
       char name[30];
       float volume;
       double price;
   }
   inflatable guest = 
   {
       "Glorious Gloria",
       1.88,
       38.88
   }
   ```

2. 结构说明
   * 可以将结构作为参数传递给函数
   * 可以让函数返回一个结构
   * 可以使用赋值运算符，将结构赋值给另一个结构 (成员赋值)
3. 结构数组
   
   * `inflatable fifts[100];`

## 共用体

* 能够存储不同的数据类型，但只能同时存储其中一种类型。

* 共用体语法

  ```c
  union one {
      int int_val;
      long long_val
  }
  ```

## 枚举

1. 创建符号常量的方式，可以代替const
   * `enum spectrum {red, orange, yellow, green};`
2. 设置枚举的值
   * `emum color {red, orange=100, green}`

## 指针和自由存储空间

1. 存储空间
   * `*`运算符被称为解除引用运算符，可以得到地址处的值
   * `&`取地址运算符，可以得到变量的地址
2. 指针声明
   1. `int *ptr;`
   2. `int *p1, p2;`
3. 使用new来分配内存
   * `int * pt = new int;`
4. 使用delete释放内存
   * `delete ps;`
5. 使用new创建动态数组
   * `int * ps = new int [10];`
   * `delete []ps;`

 ## 指针和数组运算

* 数组名相当于首元素地址。
  * `double * pw = &wages[0]`
* 对于数组名使用sizeof得到的是数组的长度
* 对于数组名取地址时，得到的是指向整个数组的地址

## 动态创建结构

* 动态创建结构
  * `inflatable * ps = new inflatable`

## 数组的替代品

1. vector

   * 也是一种动态数组，类似string,可以在运行阶段设置vector的长度。

   * 可以在末尾添加数据，中间插入数据

   * 用法

     ```c++
     #include <vector>
     
     using namespace std;
     vector<int> vi;
     int n;
     cin >> n;
     vector<double> vd(n)
     
     ```

2. 模板类 array

   * vector类功能强大，但是付出的代价是效率稍低

   * 可以使用新增的模板类array, 也位于命名空间std中。(固定长度，使用栈空间)

   * 基本使用

     ```c++
     #include <array>
     
     using namespace std;
     array<int, 5> ai;
     array<double, 5> ad = {1.2, 4.3, 52, 5};
     ```

     

