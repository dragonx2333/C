左旋字符串中k个字符

~~~c
#include<stdio.h>
#include<assert.h>
#include<string.h>

// 反转数组中指定长度的部分
void reverse(char* arr, int n)
{
	int left = 0,
		right = n - 1;
	while (left < right)
	{
		int tmp = arr[left];
		arr[left] = arr[right];
		arr[right] = tmp;
		left++;
		right--;
	}
}

//三步反转法：
//以反转abcde前两个字符为例
//第一步bacde
//第二步baedc
//第三步cdeab
void left_move(char* arr, int k)
{
	assert(arr);
	int len = strlen(arr);
	assert(k <= len);
	reverse(arr, k);          // 反转前 k 个字符
	reverse(arr + k, len - k);// 反转剩下的字符
	reverse(arr, len);        // 反转整个字符串

}

int main()
{
	char arr[] = "abcdefghij";
	int k = 0;
	printf("%s\n", arr);
	printf("请输入您要左旋的字符串个数：");
	scanf_s("%d", &k);
	left_move(arr, k);
	printf("左旋后的字符串为：\n%s", arr);
	return 0;
}
~~~

