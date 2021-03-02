### 题目描述

 N<k时，root(N,k) = N，否则，root(N,k) = root(N',k)。N'为N的k进制表示的各位数字之和。输入x,y,k，输出root(x^y,k)的值 (这里^为乘方，不是异或)，2=<k<=16，0<x,y<2000000000，有一半的测试点里 x^y 会溢出int的范围(>=2000000000) 

#### 输入描述

> ```c++
> 每组测试数据包括一行，x(0<x<2000000000), y(0<y<2000000000), k(2<=k<=16)
> ```

#### 输出描述

> ```c++
>  输入可能有多组数据，对于每一组数据，root(x^y, k)的值
> ```

### 示例

输入：

```c++
4 4 10
```

输出：

```c++
4
```

### 思路

乘方可以使用[乘法快速幂](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/solution/c-cheng-fa-kuai-su-mi-by-yizhe-shi/)，可以看看我在 leetcode 上的题解。

因为可能会溢出 int，那么我们使用 long long

对于root（N，k），根据题意有 $N = a_0 + a_1k + a_2k^2 +...,N' = a_0 + a_1 + a_2+ ...$

$N-N'=a_1(k-1)+a_2(k^2-1)...\to(N-N')\%(k-1)=0$

同理可得 $(N'-N'')\%(k-1)=0$，依次类推，$(N-N_n^{'})\%(k-1)=0$

因为最后 $N'<k$，所以$N'=N\%(k-1)$，如果$N\%(k-1)==0$，说明$N'=k-1$

```c++
#include<iostream>

using namespace std;

long long quickpower(long long x, long long y, int k){
    long long ans = 1, temp = x;
    while(y){
        if(y & 1) ans = ans * temp % (k - 1);
        temp = temp * temp % (k - 1);
        y >>= 1;
    }
    return ans ? ans : k - 1;
}

int main(){
    int x, y, k;
    while(cin >> x >> y >> k){
        cout << quickpower(x, y, k) << endl;
    }
    return 0;
}
```

