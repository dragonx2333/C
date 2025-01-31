判断质数

~~~c
#include<stdio.h>
#include <math.h>

int is_prime(int n)
{
	int i = 0;
	for (i = 2; i <= sqrt(n); i++)
	{
		if (n % i == 0)
		{
			return 1;
		}
	}
	return 0;
}

int main()
{
	int n = 0;
	while (1)
	{
		printf("请输入要判断的数字：");
		scanf_s("%d", &n);
		if (n < 0)
		{
			printf("输入无效，请输入正数\n");
		}
		else 
		{
			if (is_prime(n))
			{
				printf("不是素数\n");
			}
			else
			{
				printf("是素数\n");
			}
		}
	}
	return 0;
}
~~~

