判断输出结果：(与strlen和sizeof以及指针相关的一些题)

1.

~~~c
#include<stdio.h>

int main()
{
	char a[1000] = { 0 };
	int i = 0;
	for (; i < 1000; i++)
	{
		a[i] = -1 - i;
		//-1,-2,-3,...,-128,127,...,1,0,...
		//strlen检测到0就停止遍历了
	}
	printf("%d", strlen(a));//255
	return 0;
}
~~~

2.

~~~c
int main()
{
	int arr[] = { 1,2,3,4,5 };
	printf("%d\n", strlen(arr));//随机值
	printf("%d\n", strlen(arr + 0));//随机值
	printf("%d\n", sizeof(arr));//20
	printf("%d\n", sizeof(arr + 0));//4/8(地址)
	printf("%d\n", strlen(*arr));//error
	return 0;
}
~~~

3.

~~~c
int main()
{
	char* p = "abcdef";
	printf("%d\n", sizeof(p + 1));//4/8(b的地址)
	printf("%d\n", sizeof(p[0]));//1
	int a[3][4] = { 0 };
	printf("%d\n", sizeof(a[0] + 1));//4/8(a[0][1]的地址)
	printf("%d\n", sizeof(a + 1));//4/8（第二行的地址)
	printf("%d\n", sizeof(&a[0] + 1));//同第一个
	printf("%d\n", sizeof(a[3]));//不会报错，16
	return 0;
}
~~~

4.

~~~c
int main()
{
	int arr[3][2] = { (0,1),(2,3),(4,5) };
	//逗号表达式，实际上arr是{{1，3}，{5，0}，{0，0}}
	int* p = arr[0];
	printf("%d", p[0]);//相当于arr[0][0]
}
~~~

5.

~~~c
int main()
{
	int a[5][5];
	int (*p)[4];
	p = a;
	printf("%p,%d\n", &p[4][2] - &a[4][2], &p[4][2] - &a[4][2]);
	//两地址相减结果为-4，其补码为1111...11100,若打印的是地址，
	//则直接打印其16进制形式FFFFFFFC
}
~~~

![image-20250107153755503](C:\Users\洋洋\AppData\Roaming\Typora\typora-user-images\image-20250107153755503.png)

6.

~~~c
int main()
{
	char* c[] = { "ENTER" ,"NEW","POINT","FIRST" };
	char** cp = { c + 3, c + 2, c + 1, c };
	char*** cpp = cp;
	printf("%s\n", **++cpp);//此时cpp指向c+2
	printf("%s\n", *-- *++cpp + 3);//此时cpp指向c+1，并且+3在最后执行
	printf("%s\n", *cpp[-2] + 3);//*cpp[-2]指的是**(cpp-2)
	printf("%s\n", cpp[-1][-1] + 1);//指的是*(*(*(cpp-1)-1)+1)
	return 0;
}
~~~

![image-20250107170323328](C:\Users\洋洋\AppData\Roaming\Typora\typora-user-images\image-20250107170323328.png)

![image-20250107170810030](C:\Users\洋洋\AppData\Roaming\Typora\typora-user-images\image-20250107170810030.png)

![image-20250107170843584](C:\Users\洋洋\AppData\Roaming\Typora\typora-user-images\image-20250107170843584.png)

7.

~~~c
#include<stdio.h>

int main()
{
	char a[4] = { 0 };
	struct b
	{
		char x;
		char y : 1;
		char z : 2;
		char l : 3;
	}*c;
	c = (struct b*)a;
	c->x = 2;
	c->y = 3;
	c->z = 4;
	c->l = 5;
    //a[0]:00000010 a[1]:00101001
	printf("%02x %02x %02x %02x\n", a[0], a[1], a[2], a[3]);
	//          02 29 00 00
	return 0;
}
~~~

![image-20250123174417156](C:\Users\洋洋\AppData\Roaming\Typora\typora-user-images\image-20250123174417156.png)

