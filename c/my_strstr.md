~~~c
#include<stdio.h>
#include<assert.h>

char* my_strstr(const char* str1, const char* str2)
{
	assert(str1 && str2);
	char* cur = str1;
	//以abbbcde，bbc为例，若不设置cur这个临时变量，
	//会因为bbb和bbc无法匹配而直接判定返回NULL，
	//所以我们需要每个大循环都只前进一个字符，
	//每次大循环都进行一边匹配，这样既满足了返回
	//目标指针的要求，又实现了正确的寻找
	char* s1 = NULL;
	char* s2 = NULL;
	//先处理str2为空的情况
	if (!*str2)
	{
		return (char*)str1;
	}
	while (*cur)
	{
		s1 = cur;
		s2 = str2;
		while (s1 && s2 && (*s1 == *s2))
			//匹配
		{
			s1++;
			s2++;
		}
		//匹配成功
		if (!*s2)
		{
			return cur;
		}
		//若不成功，cur前移1字节
		cur++;
	}
	return NULL;
}
~~~

