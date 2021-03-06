### 题目描述

求正整数N(N>1)的质因数的个数。 相同的质因数需要重复计算。如120=2\*2\*2\*3\*5，共有5个质因数。

#### 输入描述

> ```c++
> 可能有多组测试数据，每组测试数据的输入是一个正整数N，(1<N<10^9)。
> ```

#### 输出描述

> ```c++
> 对于每组数据，输出N的质因数的个数。
> ```

### 示例

输入：

```c++
120
```

输出：

```c++
5
```

### 思路

我们求质因子的时候其实没有必要去先判断一个因子是否为质数，为什么呢？

比如说一个因子为 11，是质数，那么无论前面怎么进行除法运算，一定有这个因子，所以质数因子不可能漏掉

而对于因子 4，它肯定可以转换成质因子之积：2×2，那么在前面已经被除过了，所以已经没有非质数因子了

所以我们只需要从 2 开始遍历，遍历到 $\sqrt{n}$ 即可，为什么是 $\sqrt{n}$ 呢？

因为一个数字至多存在一个大于 $\sqrt{n}$ 的因子，所以如果存在大于 $\sqrt{n}$ 的因子，加一就好了。

```c++
#include<iostream>
#include<cmath>
using namespace std;

int main(){
    int num;
    while(cin >> num){
        int cnt = 0;
        for(int i = 2; i <= sqrt(num); i ++){
            while(num % i == 0){
                cnt ++;
                num /= i;
            }
            if(num <= 1) break;
        }
        // 存在大于 sqrt(num) 的因子
        if(num > 1) cnt ++;
        cout << cnt;
    }
    return 0;
}
```





