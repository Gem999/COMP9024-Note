# week1

## String

String is a special word for an array of characters:

​		end-of-string is denoted by '\0'

Example:

If a character array s[11] contains the string "hello",then is would look in memory:

​    0	1	2	3	4	5	6	7	8	9	10

​    **h	e	 l	 l	o	\0**

## Reading variable values with scanf()  and atoi()

### scanf

scanf(format-string, expr1, expr2);

i.e.  scanf("%s", str);

tips: 将输入的内容作为字符串

### atoi(string)

int value = atoi(string);

这是将字符串变成整数的方法

## Arrays and Function

When an array is passes as parameter to a function, the address of the start of the array is actually passed.

Example:

int total, vec[20];

total = sum(vec);  ( the address the the start of array vec, and the size of array is not known)



Therefore, the size of the array should be passes as an extra parameter

Example:

int sum(int[], int)

## Defining New Data Types

C allows us to define new data typee via typedef;

**typedef ExistingDataType NewTypeName;**

Example:

typedef float Temperature;

## Structures

structure is a collection of variables, perhaps of different types

``` c
typedef struct {
    char name[30];
    int zID;
} StudentT;

typedef struct {
    int day, month;
} DateT;

typedef struct {
    int hour, minute;
} TimeT;

typedef structure {
    char plate[7];
    double speed;
    DataT d;
    TimeT t;
} TicketT;

## Defining a structured data type itself does not allocate any memory
## we need to decalre a variable in order to allocate memory
DateT christmas;
## The compoents of the structure can be accessed using the 'dot' operator
christmas.day = 25;
christmas.month = 12;
```

## ADT vs ADO

### ADT

ADT： Abstract Data Types

ADT is a logical description of how we view the data and the operations

### ADO

ADO: Abstract data object

ADO include **stack** and **queue**

#### Stack

LIFO: last in, first out

Application: 

​	undo sequence in the text editor

​	bracket matching algorithm

#### Queue

FIFO: first in, first out

Applications:

​	the checkout at a supermarket

​	people queueing to go onto a bus

​	chat message

​	web page request arriving at a web server

### *static

1. 局部变量

   1).**普通局部变量**是再熟悉不过的变量了，在任何一个函数内部定义的变量（不加static修饰符）都属于这个范畴。编译器一般不对普通局部变量进行初始化，也就是说它的值在初始时是不确定的，除非对其显式赋值。

   2).**静态局部变量**使用static修饰符定义，即使在声明时未赋初值，编译器也会把它**初始化为0**。且静态局部变量存**储于进程的全局数据区**，即使函数返回，它的值也会保持不变。

2. 全局变量

   全局变量定义在函数体外部，在全局数据区分配存储空间，且编译器会自动对其初始化。

   普通全局变量对整个工程可见，其他文件可以使用extern外部声明后直接使用。也就是说其他文件不能再定义一个与其相同名字的变量了（否则编译器会认为它们是同一个变量）。

   静态全局变量仅对当前文件可见，其他文件不可访问，其他文件可以定义与其同名的变量，两者互不影响。

   **在定义不需要与其他文件共享的全局变量时，加上static关键字能够有效地降低程序模块之间的耦合，避免不同文件同名变量的冲突，且不会误使用。**

3.函数

函数的使用方式与全局变量类似，在函数的返回类型前加上static，就是静态函数。其特性如下：

- 静态函数只能在声明它的文件中可见，其他文件不能引用该函数
- 不同的文件可以使用相同名字的静态函数，互不影响

下面两个文件的例子说明使用static声明的函数不能被另一个文件引用：

```c
/* file1.c */
#include <stdio.h>

static void fun(void)
{
    printf("hello from fun.\n");
}

int main(void)
{
    fun();
    fun1();

    return 0;
}

/* file2.c */
#include <stdio.h>

static void fun1(void)
{
    printf("hello from static fun1.\n");
}
```

```c
/* file1.c */
#include <stdio.h>

void fun(void)
{
    printf("hello from fun.\n");
}

/* file2.c */
int main(void)
{
    fun();

    return 0;
}
```

### *assert

assert(test) terminates program with error message if test fails

```c
#include "stack.h"
#include <assert.h>

//define the Data Structure
typedef struct{
    char item[MAXITEMS];
    int top;
} stackRep;

//define the Data Object
static stackRep stackObject;

//set up empty stack
void StackInit(){
    stackObject.top = -1;
}

//check whether stack is empty
int StackIdEmpty(){
    return (stackObject.top < 0);
}

//insert char on top of stack
void StackPush(char ch) {
    assert(stackObject.top < MAXITEMS -1);   //判断内存是否够用
    stackObject.top++;
    int i = stackObject.top;
    stackObject.item[i] = ch;
}

//remove char from the top of stack
char StackPop(){
    assert(stackObject.top > -1);   //判断是否是空栈
    int i = stackObject.top;
    char ch = stackObject.tiem[i];
    stackObject.top--;
    return ch;
}
```







