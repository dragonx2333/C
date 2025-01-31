strtok使用示例

~~~c
#include <stdio.h>
#include <string.h>

int main() 
{
    char str[] = "Hello, World!How are you?";
    const char p[] = " ,!"; // 分隔符字符串
    char* ret = NULL;
    // 第一次调用strtok函数
    ret = strtok(str, p);
    // 通过循环继续分割字符串
    while (ret != NULL)
    {
        printf("%s ", ret); // 打印分割出的子字符串
        ret = strtok(NULL, p); // 继续分割剩余的字符串
    }
    //也可以用for循环
    return 0;
}
~~~

~~~c
char * strtok(char *str, const char *delim);
~~~

strtok工作原理：

strtok函数在参数str的字符串中发现参数delim中包含的分割字符时，会将该字符改为字符串结束符'\0'。

在第一次调用时，strtok函数必需给予参数str一个需要进行分割的字符串，往后的调用则应将参数str设置成NULL。

strtok函数使用一个静态的内部变量（或称为“静态内部缓冲区”）来跟踪当前处理的位置