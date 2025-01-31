strlen的三种自定义写法：

递归

~~~c
#include<stdio.h>

int my_strlen(char* str)
{
	if (*str)
	{
		return 1 + my_strlen(str + 1);
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



指针 -指针 = 二者之间的元素总数(由于char大小就是1字节，所以不需要区分元素和字节的区别了)

~~~c
#include<stdio.h>

int my_strlen(char* str)
{
	char* start = str;
	char* end = str;
	while (*end)
	{
		end++;
	}
	return end - start;
}

int main()
{
	char arr[] = "abcdef";
	printf("%d", my_strlen(arr));
	return 0;
}
~~~



计数器

~~~c
#include <stdio.h>

int my_strlen(char* str)
{
    int n = 0;
    while (*str)
    {
        n++;
        str++;
    }
    return n;
}
~~~

