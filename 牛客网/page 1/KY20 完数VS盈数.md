### 题目描述

一个数如果恰好等于它的各因子(该数本身除外)子和，如：6=3+2+1。则称其为“完数”；若因子之和大于该数，则称其为“盈数”。 求出2到60之间所有“完数”和“盈数”。

#### 输入描述

> ```c++
> 题目没有任何输入。
> ```

#### 输出描述

> ```c++
> 输出2到60之间所有“完数”和“盈数”，并以如下形式输出：
> E: e1 e2 e3 ......(ei为完数)
> G: g1 g2 g3 ......(gi为盈数)
> 其中两个数之间要有空格，行尾不加空格。
> ```

### 示例

输入：

```c++

```

输出：

```c++

```

### 思路

求出 2 到 60 之间数字的因子之和，然后进行比较，判断出是完数还是盈数，并用两个数组分别去存储。

```c++
#include<iostream>
#include<vector>

using namespace std;

int judge(int num){
    int sum = 0;
    for(int i = 1; i < num; i ++){
        if(num % i == 0)
            sum += i;
    }
    if(sum == num) return 1;
    if(sum > num) return 0;
    return -1;
}

int main(){
    vector<int> e, g;
    for(int i = 2; i <= 60; i ++){
        if(judge(i) == 1) e.push_back(i);
        else if(judge(i) == 0) g.push_back(i);
    }
    cout << "E:";
    for(int i : e) cout << " " << i;
    cout << endl;
    cout << "G:";
    for(int i : g) cout << " " << i;
    return 0;
}
```

