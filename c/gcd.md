~~~c
#include<stdio.h>

int main()
{
	int m = 0,
		n = 0,
		r = 0;
	scanf_s("%d%d", &m, &n);
	while (r = m % n)
	{
		m = n;
		n = r;
	}
	printf("%d", n);
	return 0;
}
~~~

