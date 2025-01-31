goto语句的用法以及system的一些用法

~~~c
#include<stdio.h>
#include<string.h>
#include<stdlib.h>

int main()
{
	char input[] = { 0 };
	system("shutdown -s -t 60");//"shutdown" 是 Windows 中用来关闭计算机的命令
	//-s 参数指示"shutdown"命令执行关机操作（shutdown 的意思是关闭，而 - s 参数具体指的是关机）
	//- t 60 参数设置关机操作在指定的秒数之后执行，这里的60表示计算机将在命令执行后的60秒内关机
    again://是冒号不是分号
	printf("您的电脑将在60s后关机，若输入；操作错误，就取消关机\n请输入：");
	scanf("%s", input);
	if (!strcmp(input, "点错了"))
	{
		system("shutdown -a");//中止之前通过"shutdown"命令发起的系统关机或重启操作
		//这里的-a参数代表 "abort"（中止）。
	}
	else
	{
		printf("输入'点错了'取消关机\n");
		goto again;
	}
	return 0;
}
~~~

