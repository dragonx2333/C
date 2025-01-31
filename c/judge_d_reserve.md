写一个函数，实现判断一个字符是否是由另一个字符串左旋而来：

~~~c
#include<stdio.h>
#include<string.h>

int is_left_move(char* str1, char* str2)
{
	//将原始字符串拼接上自身的一个复制得到的新字符串
	//包含了所有该字符串的左旋版本，
	//所以直接在这个新字符串中搜索目标字符串来判断。
	int len1 = strlen(str1);
	int len2 = strlen(str2);
	if (len1 != len2)
	{
		return 0;
	}
	strncat(str1, str1, len1);
	//如果直接使用strcat，会导致原字符串'\0'的丢失，
	//致使自复制出错，所以要使用strncat控制复制数量
	char* ret = strstr(str1, str2);
	//strstr返回值是该字符串在原始字符串第一次出现位置的指针或NULL
	if (ret)
	{
		return 1;
	}
	return 0;
}

int main()
{
	char arr1[100] = { 0 };
	printf("请输入源字符串：");
	scanf("%s", arr1);
	char arr2[100] = { 0 };
	printf("请输入要判断的字符串：");
	scanf("%s", arr2);
	if (is_left_move(arr1, arr2))
	{
		printf("第二个字符串是由第一个字符串左旋而来\n");
	}
	else
	{
		printf("第二个字符串不是由第一个字符串左旋而来\n");
	}
	return 0;
}
~~~

在自复制过程中可能会导致缓冲区溢出，以下是更好的临时变量自复制方法：

~~~c
    // 创建一个足够大的缓冲区来存储 str1 + str1
    char temp[2 * len1 + 1]; // +1 是为了存储末尾的 '\0'
    strcpy(temp, str1); // 复制 str1 到 temp
    strcat(temp, str1); // 再次复制 str1 到 temp 的后半部分
~~~

