~~~c
#include<stdio.h>
#include<assert.h>

int my_strcmp(const char* str1, const char* str2)
{
	assert(str1 && str2);
	while (*str1 == *str2)
	{
		if (!*str1)
		{
			return 0;
		}
		str1++;
		str2++;
	}
	//若是gcc，则直接写return *str1 - *str2
	if (*str1 > *str2)
	{
		return 1;
	}
	else
	{
		return -1;
	}
}
~~~

my-strncmp

~~~c
#include<stdio.h>
#include<assert.h>

int my_strncmp(const char* str1, const char* str2, int num)
{
	assert(str1 && str2);
	int i = 0;
	while (i < num)
	{
		//若是gcc，则直接写return *str1 - *str2
		if (*str1 > *str2)
		{
			return 1;
		}
		else if(*str1 < *str2)
		{
			return -1;
		}
		str1++;
		str2++;
		i++;
	}
	return 0;
}
~~~

