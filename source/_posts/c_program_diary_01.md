---
title: C program 日记01-理解const和引出的问题
tag: [GCC,const,pointer,misunderstanding]
category: C语言日记
date: 2016-09-18
---

# 理解const和引出的问题
**2016.9.18 重庆 多云**

开始拾起原来的一些东西，并且纠正自己原来一些不够深入的理解,从C语言开始。

### const关键字

C中的`const`关键字和JAVA中的`final`关键字有着相似的功能，表示被修饰的对象（不是面向对象中的”对象”）的内容不会变化，被修饰的函数不会有副作用。

### const修饰字符串指针

```c
const char *o = "hello there";
char const *o = "hello there";
char* const q = "hello there";

o[0] = 'o';
p[0] = 'p';
q[0] = 'q';
```

对于上述的三种字符串声明方式，gcc都是可以编译通过的。

但是对于三种修改字符串值的方法都是错误的：第一种和第二种编译不会通过，第三种编译通过，运行出现**segment fault**错误。

原因：

前两种声明方法效果是相同，都是声明了一个指向**const characters**的pointer，所以`const`修饰的是`*o`而不是`o`，即修饰的是”hello there”，所以`o[0] = 'o';`或者`p[0] = 'p';`对const characters进行修改是不被允许的，所以在gcc的语意分析(我猜的)被发现而不通过编译。

第三种声明方式，则是声明了一个指向characters的**const pointer**，所以`const`修饰的是`o`而不是characters，于是`q[0] = 'q'`在语意上是正确的，所以gcc编译通过。

### 对指针的一点理解

原来我以为`char *`可以看作是一种数据类型，比如字符串指针类型，这是当时的有偏差的理解，其实`*`一直都是指针运算符，且`*`运算符的优先级大于`=`，所以我认为此处`char *o = "hello there";`先声明了”指针变量”`o`,并且要赋值`o`,但用户没有能力来管理指针`o`的确值，所以c语言就提供了间接的方式，及`*o = "hello there"`，及指针`o`的取值是字符串”hello there”的地址，然后使用`char`来限定使用`*(o+1)`,`o[1]`来取值时值存储大小，偏移大小等问题。

### 关于segment fault

维基百科对于[segment fault](https://en.wikipedia.org/wiki/Segmentation_fault)造成的原因有列举:

> 1.Writing to read-only memory
> 2.Null pointer dereference
> 3.Buffer overflow
> 4.Stack overflow

对于第三种`q[0] = 'q';`，发生segment fault的原因是上述第一种原因。
使用`strace`或者`gdb`分析程序出错原因。

```
# part of gdb output
(gdb) r
Starting program: /home/lambor/test/test_const/a.out 
Program received signal SIGSEGV, Segmentation fault.
0x0000000000400501 in main () at test.c:3
3		q[0] = 'q';
(gdb) print q
$1 = 0x400594 "hello there"
```

发现错误代码时，变量`q`的值为0x400594，即字符串”hello there”分布在内存0x400594处。

然后使用`objdump`来查看程序的段分布。
```
# part of objdump output
$ objdump -h ./a.out
Idx Name          Size      VMA               LMA               File off  Algn
...
 14 .rodata       00000012  0000000000400590  0000000000400590  00000590  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
...
```

所以字符串”hello there” 位于 “.rodata” 段,数据是只读, 所以修改会触发segment fault。


### 关于mutable characters

我首先想到 gcc 的 “attribute“机制，将数据放入 writeable 段中，比如”.data”段

首先 attribute((section())) 不能修饰局部变量。

我的两种错误尝试：

```
char * const q = "hello, world!" __attribute__((section(".data")));
```
语法不正确，编译不通过的。

```
char * const q __attribute__((section(".data"))) = "hello, world!" ;
```
语意不正确，而且编译器直接报warning，并忽略。

后来通过查找，发现[老版本的gcc (version <= 4)支持功能 writeable-strings clarification](https://gcc.gnu.org/ml/gcc/2005-04/msg01257.html)。

需要使用”-fwriteable-strings”。但是现在取消了该功能，建议使用

```
char mutable_chars[] = {"hello there"};
mutable_chars[0] = 'p';
```


