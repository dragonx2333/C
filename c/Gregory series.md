打印1/1-1/2+1/3-...

~~~c
#include<stdio.h>

int main()
{
	int i = 0,
		n = 0,
		flag = 1;
	double sum = 0;
	scanf("%d", &n);
	for (i = 1; i <= n; i++)
	{
		sum += flag * 1.0 / i;
		//加上1.0算的才是小数
		flag = -flag;
	}
	printf("%d", sum);
	return 0;
}
~~~

