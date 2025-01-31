strerror的使用示例

~~~c
#include <stdio.h>
#include <string.h>
#include <errno.h>

int main()
{
    FILE* file = fopen("nonexistent.txt", "r");
    if (!file) 
    {
        printf("Error opening file: %s\n", strerror(errno));
        //在这个示例中，如果fopen函数调用失败（例如，因为文件不存在），
        //errno 将被设置为一个表示错误的代码，然后，
        //strerror函数被用来将这个错误代码转换为一个可读的错误消息字符串，
        //该字符串随后被打印出来
    }
    return 0;
}
~~~

