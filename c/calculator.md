函数指针应用之一：

转移表（简化多选择函数）

~~~c
#include<stdio.h>

int Add(int x, int y)
{
	return x + y;
}

int Sub(int x, int y)
{
	return x - y;
}

int Mul(int x, int y)
{
	return x * y;
}

int Div(int x, int y)
{
	return x / y;
}

void menu()
{
	printf("**********************************\n");
	printf("*******1.Add           2.Sub******\n");
	printf("*******3.Mul           4.Div******\n");
	printf("*******       0.exit        ******\n");
	printf("**********************************\n");
}

int main()
{
	int(*pfArr[])(int, int) = { 0,Add,Sub,Mul,Div };
	int input = 0,
		x = 0,
		y = 0;
	do
	{
		menu();
		printf("请选择：");
		scanf("%d", &input);
		if (input >= 1 && input <= 4)
		{
			printf("请输入两个操作数：");
			scanf("%d%d", &x, &y);
			int ret = pfArr[input](x, y);
			printf("结果为%d\n", ret);
		}
		else if (input == 0)
		{
			printf("退出计算器\n");
		}
		else
		{
			printf("输入错误，请重新输入\n");
		}
	} while (input);
	return 0;
}
~~~

