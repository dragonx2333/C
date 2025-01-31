### 一、带有副作用的宏

~~~c
#include<stdio.h>

#define MAX(a,b) ((a)>(b)?(a):(b))

int main()
{
	int a = 11,
		b = 12,
		c = MAX(a++,b++);
    //((a++)>(b++)?(a++):(b++))
    //第二个a++不执行，b++两次，由于是后置++，b++一次后被赋给c
	printf("%d\n%d\n%d\n", a, b, c);
	return 0;
}
~~~

### 二、防止头文件内容的重复

1.  ~~~c
   #ifndef __TEST_H__
   #define __TEST_H__
   
   // 头文件的内容
   // ...
   
   #endif // __TEST_H__
   ~~~

2. ~~~c
   #pragma once
   ~~~

### 三、请编写一个宏，计算结构体中某变量相对于首地址的偏移

~~~c
#define OFFSETOF(struct_type,member) (int) & (((struct_type*)0) -> member)
~~~

1. **`(struct_type\*)0`**：这部分代码将数字0转换为一个指向`struct_type`类型的指针，表示一个空指针（即不指向任何有效内存地址的指针）
2. **`-> member`**：这是结构体指针访问成员的操作符。由于我们已经有一个指向`struct_type`的指针（尽管它指向的是地址0，但我们不会实际去解引用它），我们可以使用这个指针来访问结构体中的`member`成员。这里的关键是，编译器会计算出`member`相对于结构体起始地址的偏移量，而不会因为指针指向地址0而引发运行时错误

### 四、字符串化操作符`#`

~~~c
#define PRINT(X) printf("the value of " #X " is %d\n", X)
//#会被替换成宏参数X对应的字符串字面量，并且这个字符串字面量会被无缝地插入到printf的格式化字符串中。

int main()
{
	int a = 1;
	PRINT(a);
	return 0;
}
~~~