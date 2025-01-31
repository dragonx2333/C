统计非负数二进制中1的个数

法1：

~~~c
#include<stdio.h>

int count_one(unsigned int n)
{
	int count = 0;
	while (n)
	{
		if (n % 2 == 1)
		{
			count++;
		}
		n /= 2;
	}
	return count;
}

int main()
{
	unsigned int n = 0,
		ret = 0;
	printf("请输入一个非负数：");
	scanf_s("%d", &n);
	ret = count_one(n);
	printf("您输入的数字二进制表示中有%d个1\n",ret);
	return 0;
}
~~~

法2：

~~~c
int count_one(unsigned int n)
{
	int i = 0,
		count = 0;
	for (; i < 32; i++)
	{
		if (((n >> i) & 1) == 1)
		{
			count++;
		}
	}
	return count;
}
~~~

法3：（最帅的方法）

~~~c
int count_one(unsigned int n)
{
	int count = 0;
	//该方法依次降1位
	while (n)
	{
		n = n & (n - 1);
		//以11为例
		//1011
  //减一后1010
//按位与后1010
  //减一后1001
//按位与后1000
  //减一后0111	
//按位与后0000
		count++;
	}
}
~~~

根据法3延展出来的解题方法：

求两个数二进制中不同位的个数：

~~~c
#include<stdio.h>

int get_diff_bit(int m, int n)
{
	int tmp = m ^ n,
		count = 0;
	while (tmp)
	{
		tmp = tmp & (tmp - 1);
		count++;
	}
	return count;
}
~~~

