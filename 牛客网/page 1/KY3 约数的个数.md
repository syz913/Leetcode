### 题目描述

输入n个整数,依次输出每个数的约数的个数

#### 输入描述

> ```c++
> 输入的第一行为N，即数组的个数(N<=1000)
> 接下来的1行包括N个整数，其中每个数的范围为(1<=Num<=1000000000)
> ```

#### 输出描述

> ```c++
> 可能有多组输入数据，对于每组输入数据，
> 输出N行，其中每一行对应上面的一个数的约数的个数。
> ```

### 示例

输入：

```c++
5
1 3 4 6 12
```

输出：

```c++
1
2
3
4
```

### 思路

题干很简单，但是暴力方法是会超时的

对于数 n，因为小于 $\sqrt{n}$ 的数 i 如果能整除n，则必定还有一个大于 $\sqrt{n}$ 的因数j，使得 $i*j=n$，+2是把这两个因数都算进去了。最后如果 i=n，说明有两个相同的i是因数，只算一个。

```c++
#include<iostream>
using namespace std;

int numOfDivisor(int num){
	int ans = 0;
	int i;
	for (i = 1; i*i<num; i++){
		if (num%i == 0)
			ans += 2;
	}
	if (i*i == num) ans++;
	return ans;
}
int main(){
	int n, num;
	while (cin >> n)
	{
		for (int i = 0; i<n; i++)
		{
			cin >> num;
			cout << numOfDivisor(num) << endl;
		}
	}
	return 0;
}
```

这里我们引入一个约数个数定理：

若 $x=p_1^{\alpha_1}p_2^{\alpha_2}...p_n^{\alpha_n}$，其中$p_i$为质数，那么$x$的约数个数$\sigma(x)=(\alpha_1+1)(\alpha_2+1)...(\alpha_n+1)$，我们简单证明一下：对于$p_i^{\alpha_i}$来说，它的因子有$p_i^0,p_i^1,...,p_i^{\alpha_i}$，而$x$的因子，就是从每个$p_i$中选择一个$p_i$的因子来组成$x$的因子，所以根据乘法原理得证。

这样只需要先求一下质数列表，然后看一下质因子的个数就好了。