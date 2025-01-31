二分查找

~~~c
#include <stdio.h>
int main()
{
	int arr[] = { 1,2,3,4,5,6,7,8,9 };
	int left = 0,
		right = 0,
		i = 0,
		k = 0;
	for (; i < sizeof(arr) / sizeof(arr[0]); i++)
	{
		printf("%d", arr[i]);
	}
	printf("\n请输入要查找的数字：>");
	scanf_s("%d", &k);
	right = sizeof(arr) / sizeof(arr[0]) - 1;
	while (left <= right)
	{
		int mid = (left + right) / 2;
		if (arr[mid] == k)
		{
			printf("找到了，下标是%d\n", mid);
			break;
		}
		else if (arr[mid] < k)
		{
			left = mid + 1;
		}
		else
		{
			right = mid - 1;
		}
	}
	if (left > right)
	{
		printf("抱歉，您要查找的数字不存在\n");
	}
	return 0;
}
~~~

