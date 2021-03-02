### 题目描述

输入任意4个字符(如：abcd)， 并按反序输出(如：dcba)

#### 输入描述

> ```c++
> 题目可能包含多组用例，每组用例占一行，包含4个任意的字符。
> ```

#### 输出描述

> ```c++
> 对于每组输入,请输出一行反序后的字符串。
> 具体可见样例。
> ```

### 示例

输入：

```c++
Upin
cvYj
WJpw
cXOA
```

输出：

```c++
nipU
jYvc
wpJW
AOXc
```

### 思路

很简单的翻转字符串，原地转换即可。可以直接用库函数，但是不推荐。

```c++
#include<iostream>
#include<algorithm>

using namespace std;

string reverseStr(string s){
    int n = s.size();
    for(int i = 0; i < n/2; i ++)
        swap(s[i], s[n - i - 1]);
    return s;
}

int main(){
    string s;
    while(cin >> s){
        reverse(s.begin(), s.end());
        cout << s << endl;
//         cout << reverseStr(s) << endl;
    }
    return 0;
}
```

