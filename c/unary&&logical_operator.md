把11变成15再变回11（一些单目操作符的使用）

~~~c
#include<stdio.h>

int main()
{
	int a = 11;//1011
	a = a | (1 << 2);
    //1101
    //0100
  //->1111
	printf("%d\n", a);//15
	a = a & (~(1 << 2));//按位取反
    //1111
    //1011
  //->1011
	printf("%d\n", a);//11
	return 0;
}
~~~

一些逻辑操作符的应用

~~~c
#include<stdio.h>

int main()
{
	int a = 0,
		b = 2,
		c = 3,
		i=  0;
	i = a++ && ++b && c++;
	//a++本身结果是a，即是0，后面的++b等就不算了
	printf("%d\n", i);//0
	printf("%d\n", a);//1
	printf("%d\n", b);//2
	printf("%d\n", c);//3
	return 0;
}
~~~

