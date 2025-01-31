函数指针的应用之一：

回调函数（通过函数指针调用函数）



通过输入元素比较函数，实现排序任意数组的函数

~~~c
#include<stdio.h>

void Swap(char* buf1, char* buf2, int width)
{
	int i = 0;
	for (i = 0; i < width; i++)
	{
		char tmp = *buf1;
		*buf1 = *buf2;
		*buf2 = tmp;
		buf1++;
		buf2++;
	}
}

void bubble_sort(char* base, int sz, int width,
	int(*cmp)(const void* e1, const void* e2))
    //使用const，与标准库函数保持一致
{
	int i = 0,
		j = 0;
	for (i = 0; i < sz - 1; i++)
	{
		for (j = 0; j < sz - 1 - i; j++)
		{
			if (cmp((const char*)base + j * width,
				(const char*)base + (j + 1) * width) > 0)
			{
				Swap((const char*)base + j * width,
					(const char*)base + (j + 1) * width, width);
			}
		}
	}
}
~~~

