my_strcpy

~~~c
#include<stdio.h>
#include<assert.h>

char* my_strcpy(char* dest, const char* src)
{
	assert(dest && src);
	char* ret = dest;
	while (*dest++ = *src++);
	return ret;
}
~~~

my_strncpy

~~~c
#include<stdio.h>
#include<assert.h>

char* my_strncpy(char* dest, const char* src,int num)
{
	assert(dest && src);
	char* ret = dest;
	int i = 0;
    while (i < num && src[i])
    {
        *dest = src[i];
        dest++;
        i++;
    }
    //src 字符串长度小于num时，填充剩余的字符为 '\0'
    while (i < num)
    {
        *dest = '\0';
        dest++;
        i++;
    }
	return ret;
}
~~~

