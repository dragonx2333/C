水仙花数（Narcissistic number）也被称为[超完全数字不变数](https://baike.baidu.com/item/超完全数字不变数/2495144?fromModule=lemma_inlink)（pluperfect digital invariant, PPDI）、[自恋数](https://baike.baidu.com/item/自恋数/8319599?fromModule=lemma_inlink)、[自幂数](https://baike.baidu.com/item/自幂数/4397236?fromModule=lemma_inlink)、阿姆斯壮数或[阿姆斯特朗数](https://baike.baidu.com/item/阿姆斯特朗数/7070382?fromModule=lemma_inlink)（Armstrong number），水仙花数是指一个 3 位数，它的每个数位上的数字的 3次幂之和等于它本身。 例如：1^3 + 5^3+ 3^3 = 153。水仙花数只是自幂数的一种，严格来说3位数的3次幂数才称为水仙花数。不过我们这里讨论的是广义上的水仙花数。

找出0~1000内的水仙花数：

~~~c
#include<stdio.h>
#include<math.h>

int main()
{
	int i = 0;
	for (; i < 1000; i++)
	{
		int tmp = i,
			n = 1,
			sum = 0;
		while (tmp/=10)
		{
			n++;//计算i的位数
		}
		tmp = i;
		while (tmp)
		{
			//计算每一位的n次方之和
			sum += pow(tmp % 10, n);
			//pow的参数和返回值都是double
			tmp /= 10;
		}
		if (sum == i)
		{
			printf("%d\n", i);
		}
	}
	return 0;
}
~~~



