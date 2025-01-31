用一段程序判断当前机器的字节序是什么

1.指针法

~~~c
#include<stdio.h>

int main()
{
	int a = 1;
	//在小端存储中，1为010000
	char* p = (char*) &a;
	printf("%d", *p);//取出的是01，故打印1
	return 0;
}
~~~

2.联合法

~~~c
#include<stdio.h>

int check_system()
{
	union
	{
		char c;//c永远在低地址处
		int i;
	}u;
	u.i = 1;
	return u.c;//返回1表示小端，0表示大端
}
~~~

~~~c
#include<stdio.h>

union
{
	short k;
	char i[2];
}a;

int main()
{
	a.i[0] = 1;
	a.i[1] = 2;
	printf("%d", a.k);
	//在小端字节序下，这两个字节组合成的short值将是0x0201，转换为十进制是513
	return 0;
}
~~~

