调整数组使奇数全部位于偶数的左边

~~~c
#include<stdio.h>

void move(int arr[], int sz)
{
	int left = 0,
		right = sz-1;
	while (left < right)
	{
		while (arr[left] % 2 == 1)
		{
			left++;
		}
		while (arr[right] % 2 == 0)
		{
			right--;
		}
		if (left < right)
		{
			int tmp = arr[left];
			arr[left] = arr[right];
			arr[right] = tmp;
		}
	}
}

int main()
{
	int arr[] = { 1,2,3,4,5,6,7,8,9,10 };
	int sz = sizeof(arr)/sizeof(arr[0]);
	int i = 0;
	move(arr, sz);
	for (; i < sz; i++)
	{
		printf("%d ", arr[i]);
	}
	return 0;
}
~~~

