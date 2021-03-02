### 题目描述

输入一个整数n，输出n的阶乘（每组测试用例可能包含多组数据，请注意处理）

#### 输入描述

> ```c++
> 一个整数n(1<=n<=20)
> ```

#### 输出描述

> ```c++
>  n的阶乘
> ```

### 示例

输入：

```c++
3
```

输出：

```c++
6
```

### 思路

因为 n 不超过 20，那么先求出前 20 的阶乘，加快一下计算。

```c++
#include<iostream>
#include<vector>

using namespace std;

int main(){
    vector<long long> dp(21, 1);
    for(int i = 2; i <= 20; i ++){
        dp[i] = dp[i - 1] * i;
    }
    int n;
    while(cin >> n){
        cout << dp[n] << endl;
    }
}
```

