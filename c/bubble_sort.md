只能排序数列

~~~c
#include<stdio.h>

void bubble_sort(int arr[], int sz)
{
	int i = 0,
		j = 0;
	for (; i < sz - 1; i++)
	{
		int flag = 1;//flag 应该在每次外层循环开始时重置为1
		for (j = 0; j < sz - 1 - i; j++)
		{
			if (arr[j] > arr[j + 1])
			{
				int tmp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = tmp;
				flag = 0;
			}
		}
		if (flag == 1)
		{
			break;
		}
	}
	for (i = 0; i < sz; i++)
	{
		printf("%d ", arr[i]);
	}
	printf("\n");
}

int main()
{
	int input[100] = { 0 };
	int sz = 0, 
		num = 0;
	printf("请输入最多100个整数，以空格分隔，输入非数字结束：\n");
	while (sz < 100 && scanf("%d", &num) == 1)
	{
		input[sz++] = num;
	}
	printf("排序后的数列为：");
	bubble_sort(input, sz);
}
~~~

