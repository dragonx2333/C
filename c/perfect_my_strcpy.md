满分的自定义strcpy

~~~c
#include<stdio.h>
#include<assert.h>

char* my_strcpy(char* dest, const char* src)
{
	assert(dest && src);
	char* ret = dest;//设置副本，保留原始位置
	while (*dest++ = *src++);
	//赋值表达式的结果是被赋的值，其在 while 循环中被用作条件。
	//当 *src 为 '\0' 时，赋值操作也会将 '\0' 复制到 dest，
	//并且由于 '\0' 转换为布尔值为假，循环结束
	return ret;
}
~~~

