1.my_memcpy

~~~c
#include<stdio.h>
#include<assert.h>

void* my_memcpy(char* dest, const char* src, int num)
{
	assert(dest && src);
	void* ret = dest;
	while (num--)
	{
		*(char*)dest++ = *(char*)src++;
	}
	return ret;
}
~~~

memcpy函数无法处理源内存区域和目标内存区域重叠的情况（自复制）

2.my_memmove（可以处理覆盖拷贝）

~~~c
#include<stdio.h>
#include<assert.h>

void* my_memmove(char* dest, const char* src, int num)
{
	assert(dest && src);
	void* ret = dest;
	if (dest < src)
	{
		while (num--)
		{
			*(char*)dest++ = *(char*)src++;
            //这里强制类型转换了，*src就可变了
		}
	}
	else
    //源字符串在目的字符串之后并且覆盖的时候，需从后往前复制
    //非覆盖情况下怎么整都行
	{
		while (num--)
		{
			*(char*)(dest + num) = *(char*)(src + num);
		}
	}
	return ret;
}
~~~

3.memset:void *memset(void *ptr, int value, size_t num);

将ptr填充为num个字节的value

4.memcmp