### C与C++
- C面向过程，是结构化的程序设计语言。
- C++面向对象，具有继承、多态和封装的特性。

### 编译过程
1. 预处理
  - 宏替换
  - 头文件展开
  - 去掉注释
  - 输出.i文件
2. 编译
  - 由编译器（gcc）完成，生成汇编文件（.s）
3. 汇编
  - 由汇编器（as）完成，生成目标文件（.o）
4. 链接
  - 由链接器（ld）完成，生成可执行文件

### 指针&引用
1. 指针存的是对象地址，本身是变量，可以更改
2. 引用是给变量起别名，一经初始化，不可更改绑定
3. 如果确认只是使用某个变量的别名，就使用引用；如果只是暂时指向某个变量，有可能还会指向其他变量甚至需要为空时，就使用指针。

### static
1. 修饰全局变量
2. 修饰局部变量，该变量只初始化一次，生命周期直到程序结束
3. 修饰普通函数，该函数仅在该文件中使用，外部文件不能访问
4. 修饰成员变量，该变量在第一次创建对象时初始化，且与其他对象共享该变量，只有一份存储，可以通过类名访问，也可以通过对象访问。
5. 修饰成员函数，该函数只能访问静态成员变量和调用静态成员函数，可以通过类名进行访问。

### const
1. 修饰普通变量，表示该变量不可更改
2. const int *p和int * const p含义不同，前者修饰指向的对象，后者修饰指针；类似的还有const int * const p
3. 修饰成员变量，该变量已经初始化，不可更改
4. 修饰函数返回值，一般返回一个常引用，表示只读
5. 修饰函数本身，表示该函数只能对成员变量进行读操作，以及只能调用常成员函数。

### volatile
1. 编译器优化有可能将某个变量a放入寄存器，这就导致存在这样一个问题：第一次从内存读取a，然后放入寄存器，后面继续访问时，就会从寄存器访问，当由于某种原因导致内存中的a被修改时，从寄存器将读取未更新的值。
2. 被修饰的变量不再被编译器进行优化，每次都从内存中获取值
3. 使用场景：
  - 多线程下，共享的标识符
  - 存储器映射的硬件寄存器通常也要加volatile说明，因为每次对它的读写都可能由不同意义
  - 中断服务程序中修改的供其它程序检测的变量需要加volatile

### mutable
1. 由于const成员函数无法修改成员变量，但是某些场景下需要进行修改，而mutable修饰的成员变量，可以在const成员函数中被修改。
2. 使用场景：
  - 多线程下，再使用互斥锁时，使用mutable修饰互斥锁成员变量，在const成员函数中就可以获取锁，从而实现现场安全。
  - 一般，不影响对象状态的成员变量可以使用mutable进行修饰，从而在const成员函数中进行写操作。

### 容器
#### vector
##### 1. emplace
```
// vector::emplace
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myvector = {10,20,30};

  auto it = myvector.emplace ( myvector.begin()+1, 100 );
  myvector.emplace ( it, 200 );
  myvector.emplace ( myvector.end(), 300 );

  std::cout << "myvector contains:";
  for (auto& x: myvector)
    std::cout << ' ' << x;
  std::cout << '\n';

  return 0;
}
```
在指定位置上添加一个元素，并返回该元素的迭代器。它会导致其后的迭代器失效。

##### 2. empalce_back
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myvector = {10,20,30};

  myvector.emplace_back (100);
  myvector.emplace_back (200);

  std::cout << "myvector contains:";
  for (auto& x: myvector)
    std::cout << ' ' << x;
  std::cout << '\n';

  return 0;
}
```
不同于push_back，emplace_back会使用传入的元素构造对象，而不是先创建临时对象。
#### list

#### queue

#### map & set
##### 1. key_compare & value_comp

##### 2. emplace & emplace_hint
```
map<int, string> my_map;
ret1 = my_map.emplace(1, "abc"); // 直接使用abc进行string对象构造
my_map.insert({1, "cdb"}); // 先创建string(cdb)临时对象，再调用移动构造函数
ret2 = my_map.emplace_hint(my_map.end(), 1, "abc");
// emplace和emplace_hint的返回值是一个pair<map::iterator, bool>
// first为被插入元素的迭代器，second为插入是否成功（key已存在，则插入失败）
```
##### 3. lower_bound & upper_bound

#### unordered_map & unordered_set

#### array

#### priority_queue

### 类
#### 权限
#### struct & class
#### static & non-static
#### const
#### 构造函数&析构函数
#### 拷贝构造、赋值运算符
#### 移动拷贝构造、移动赋值运算
#### 重载、覆盖、重写
#### 虚函数&多态
#### this
#### 初始化列表
#### 友元
#### 单继承、多继承
#### 对象模型
### new、delete、delete[]

### 左值&右值

### 完美转发

### 智能指针

### 闭包

### 内存管理
