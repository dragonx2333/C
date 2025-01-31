~~~c
#include<stdio.h>

int main()
{
	int n = 0;
	scanf_s("%d", &n);
	//函数的链式访问指的是返回值做参数
	//嵌套调用是指自定义函数中用另一个自定义函数
	printf("%d", printf("%d", n));
	//printf返回值表示 printf 函数实际写入的字符总数,
	//包括所有输出的字符，如数字、字母、空格和不可见的字符（如换行符\n）
	return 0;
}
~~~

