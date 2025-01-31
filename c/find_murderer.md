找出凶手，以下为4个嫌疑犯的供词：

A：不是我。

B：是C。

C：是D。

D：C在胡说。

已知只有一个人说了假话，请写一个程序来判断谁是凶手

~~~c
#include<stdio.h>

int main()
{
	char killer = 0;
	for (killer = 'a'; killer <= 'd'; killer++)//从a到d进行遍历
	{
		if ((killer != 'a') + (killer == 'c') + (killer == 'd') 
            + (killer != 'd') == 3)//真为1，假为0
		{
			printf("凶手是%c",killer);
		}
	}
	return 0;
}
~~~

