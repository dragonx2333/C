my_strcat

~~~c
#include<stdio.h>
#include<assert.h>

char* my_strcat(char* dest, const char* src)
{
	assert(dest && src);
	char* ret = dest;
	while (*dest)
	{
		dest++;
	}
	while (*dest++ = *src++);
	return ret;
}

int main() 
{
	char dest[50] = "Hello, "; // 确保 dest 有足够的空间
	const char* src = "World!";
	my_strcat(dest, src);
	printf("%s\n", dest);
	return 0;
}
~~~

my_strncat

~~~c
#include<stdio.h>
#include<assert.h>

char* my_strncat(char* dest, const char* src, int num)//库函数里写的时size_t
{
	assert(dest && src);
	char* ret = dest;
	int i = 0;
	while (*dest)
	{
		dest++;
	}
	while (i < num && src[i])
	{
		*dest = src[i];
		dest++;
		i++;
	}
	while (i < num)
	{
		*dest = '\0';
		dest++;
	}
	return ret;
}
~~~

