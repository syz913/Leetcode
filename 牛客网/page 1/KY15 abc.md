### 题目描述

设a、b、c均是0到9之间的数字，abc、bcc是两个三位数，且有：abc+bcc=532。求满足条件的所有a、b、c的值。

#### 输入描述

> ```c++
> 题目没有任何输入。
> ```

#### 输出描述

> ```c++
> 请输出所有满足题目条件的a、b、c的值。
> a、b、c之间用空格隔开。
> 每个输出占一行。
> ```

### 示例

输入：

```c++

```

输出：

```c++

```

### 思路

暴力三层循环就好了...

```c++
#include<iostream>

using namespace std;

int main(){
    for(int a = 1; a <= 9; a ++){
        for(int b = 1; b <= 9; b ++){
            for(int c = 0; c <= 9; c ++){
                if(a * 100 + b * 110 + c * 12 == 532)
                    cout << a << " " << b << " " << c << endl;
            }
        }
    }
}
```

