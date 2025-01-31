1瓶汽水1元，2个空瓶能换一瓶汽水，一个人有20元，那他能喝到多少瓶汽水

~~~c
#include<stdio.h>

int main()
{
	int money = 0,
		total = 0,
		empty = 0;
	printf("请输入您持有的钱款数量：");
	scanf("%d", &money);
	//花钱买的汽水
	total = money;
	empty = money;
	//空瓶换的汽水
	while (empty >= 2)
	{
		int new = empty / 2;
		total += new;
		empty = new + empty % 2;
	}
	printf("您总共能喝到%d瓶汽水，剩下一个空瓶", total);
	return 0;
}
//同时我们也可以用结论写
//if (money == 0)
//{
//	total = 0;
//}
//else
//{
//	total = 2 * money - 1;
//}
~~~

