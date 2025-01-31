演示多个字符从两端移动，向中间汇聚

~~~c
#include <stdio.h>
#include <string.h>
#include <windows.h>
#include <stdlib.h>
int main()
{
	char arr1[] = "Am in oac!!!";
	char arr2[] = "############";
	int left = 0,
		right = strlen(arr1) - 1;//双引号形式-->包括\0，如果是sizeof的话就是-2
	printf("%s", arr2);
	Sleep(1000);
	system("cls");
	while (left <= right)
	{
		arr2[left] = arr1[left];
		arr2[right] = arr1[right];
		printf("%s", arr2);
		Sleep(1000);
		system("cls");
		left++;
		right--;
	}
	printf("%s", arr1);
	return 0;
}

~~~

