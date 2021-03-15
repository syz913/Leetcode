### 题目描述

对给定的字符串(只包含'z','o','j'三种字符),判断他是否能AC。 是否AC的规则如下： 1. zoj能AC； 2. 若字符串形式为xzojx，则也能AC，其中x可以是N个'o' 或者为空； 3. 若azbjc 能AC，则azbojac也能AC，其中a,b,c为N个'o'或者为空；

#### 输入描述　　

> ```c++
> 输入包含多组测试用例，每行有一个只包含'z','o','j'三种字符的字符串，字符串长度小于等于1000。
> ```

#### 输出描述

> ```c++
> 对于给定的字符串，如果能AC则请输出字符串“Accepted”，否则请输出“Wrong Answer”。
> ```

### 示例

输入：

```c++
zoj
ozojo
ozoojoo
oozoojoooo
zooj
ozojo
oooozojo
zojoooo
```

输出：

```c++
Accepted
Accepted
Accepted
Accepted
Accepted
Accepted
Wrong Answer
Wrong Answer
```

### 思路

其实主要也就是 zoj 中间和两边 o 的个数的规律，标记为 left, middle, rigt

- left = right，middle = 1，可以 AC
- 由上面可以知道 nzojn (n 表示 n 个 'o') 是可以 AC 的，n ≥ 0，那么 nz 2 j (2n) 也是可以 AC 的，同样的可以知道 nz 3 j (3n) 也是可以 AC 的，以此类推，nz m j mn 是可以 AC 的，那我们就得到规律了，middle  = right/left 

```c++
#include<iostream>

using namespace std;

int main(){
    string s;
    while(cin >> s){
        int left = 0, middle = 0, right = 0;
        int n = s.size();
        int pos1 = s.find('z'), pos2 = s.find('j');
        for(int i = 0; i < pos1; i ++)
            left ++;
        for(int i = pos1 + 1; i < pos2; i ++)
            middle ++;
        for(int i = pos2 + 1; i < n; i ++)
            right ++;
        if(left == right && middle >= 1) cout << "Accepted" << endl;
        else if(left > 0 && right > 0 && right % left == 0 && middle == right/left)
            cout << "Accepted" << endl;
        else cout << "Wrong Answer" << endl;
    }
    return 0;
}
```

