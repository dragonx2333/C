接收一个无符号整型，按顺序打印它的每一位

~~~c
#include<stdio.h>

void print(int n)
{
	if (n > 9)
	{
		print(n / 10);
	}
	printf("%d", n % 10);
}

int main()
{
	int n = 0;
	scanf_s("%d", &n);
	print(n);
	return 0;
}
~~~



在不创建临时变量的情况下，求字符串长度

~~~c
#include<stdio.h>

int my_strlen(char* str)
{
	if (*str)
	{
		return 1 + my_strlen(str + 1);
		//若通过 str++ 来递增字符串指针，
		//那么str++ 表达式的结果将是一个临时值
		//它不会改变原指针 str 的值
		//因此，递归调用将永远处理同一个字符
		//导致无限递归和最终的栈溢出错误
		//所以应该使用(str + 1)来保存递增后的指针
	}
	else
	{
		return 0;
	}
}

int main()
{
	char input[100] = { 0 };
	scanf("%s", input);
	printf("%d", my_strlen(input));
	return 0;
}
~~~



另外一些类型的递归，如斐波那契数列，其递归过程会计算大量重复数据，如求第五十个数字，若使用递归，则第47个数字将会被计算2次，所以应该使用for循环



用递归实现求n的k次方：

~~~c
#include<stdio.h>

double Pow(int n, int k)
{
	if (k < 0)
	{
		return (1.0 / Pow(n, -k));
	}
	else if (k == 0)
	{
		return 1;
	}
	else
	{
		return n * Pow(n, k - 1);
	}
}

~~~

用递归实现字符串逆序：

~~~c
#include<stdio.h>
#include<string.h>

void reverse_string(char arr[])
{
	//以”abcdef"为例，逆序分为两步
	//1.af交换位置 2.bcde逆序
	char tmp = arr[0];
	int len = strlen(arr);
	arr[0] = arr[len - 1];
	arr[len - 1] = '\0';//把f变为'\0'，构成新字符串
	if (strlen(arr + 1) >= 2)
	{
		reverse_string(arr + 1);
	}
	arr[len - 1] = tmp;//在最后赋值a
}

int main()
{
	char arr[] = "abc";
	reverse_string(arr);
	printf("%s", arr);
}
~~~

以下是正常的逆序方法：

~~~c
void reverse_string(char arr[])
{
	int left = 0,
		right = strlen(arr) - 1;
	while (left < right)
	{
		char tmp = arr[left];
		arr[left] = arr[right];
		arr[right] = tmp;
		left++;
		right--;
	}
}
~~~

