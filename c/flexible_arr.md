在C99标准中，柔性数组（flexible array member）是结构体中一个特殊的成员，它表现为一个未指定大小的数组

优点：方便内存释放，有利于访问速度

特点：

1.必须为最后一个成员

2.sizeof这样的结构体返回的大小不包含柔性数组的大小

3.malloc给柔性数组开辟的空间大小 = 总大小 - 其余成员大小

~~~c
#include<stdio.h>
#include<stdlib.h>

struct S
{
	int n;
	int arr[];
};

int main()
{
	struct S* ps = (struct S*)malloc(sizeof(struct S) + 5 * sizeof(int));
	ps->n = 100;
	int i = 0;
	for (; i < 5; i++)
	{
		ps->arr[i] = i;
	}
	struct S* ptr = realloc(ps, 44);
	if (ptr)//防止内存泄漏（若开辟空间失败，则返回空指针）
	{
		ps = ptr;
	}
	free(ps);
	ps = NULL;
}
~~~

但是实际上，我们也可以用数组指针实现柔性数组的功能

~~~c
struct S
{
	int n;
	int* arr;
};

int main()
{
	struct S* ps = (struct S*)malloc(sizeof(struct S));//先开辟ps，在开辟arr
	ps->arr = (int*)malloc(5 * sizeof(int));
	int i = 0;
	for (; i < 0; i++)
	{
		ps->arr[i] = i;
	}
	int* ptr = realloc(ps->arr, 10 * sizeof(int));
	if (ptr)
	{
		ps->arr = ptr;
	}
	free(ps->arr);//注意顺序
	ps->arr = NULL;
	free(ps);
	ps = NULL;
}
~~~

