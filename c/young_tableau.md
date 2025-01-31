**`杨氏矩阵`**是一个二维数组，数组的每行从左到右是递增的，每列从上到下也是递增的。

例： 

~~~c
1 2 3
4 5 6
7 8 9
~~~

请编写一个程序，实现在一个杨氏矩阵中查找某数字是否在其中，并返回其下标：

~~~c
#include<stdio.h>

FindNum(int arr[3][3], int k, int* px, int* py)
{
	int a = *px,
		b = *py;
	*px = 0;
	(*py)--;
	while ((*px <= a - 1) && (*py >= 0))
	{
		if (arr[*px][*py] < k)
		{
			(*px)++;
		}
		else if(arr[*px][*py] > k)
		{
			(*py)--;
		}
		else 
		{
			*px = a;
			*py = b;
			return 0;
		}
		return 1;
	}
}

int main()
{
	int arr[3][3] = { {1,2,3},{4,5,6},{7,8,9} };
	int x = 3,
		y = 3;
	int k = 0;
	printf("请输入要查找的数字：");
	scanf_s("%d", &k);
	if (FindNum(arr, k, &x, &y))
	{
		printf("找到了，下标是%d%d\n", x, y);
	}
	else
	{
		printf("找不到");
	}
	return 0;
}
~~~