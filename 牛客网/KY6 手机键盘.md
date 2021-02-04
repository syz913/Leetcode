### 题目描述

按照手机键盘输入字母的方式，计算所花费的时间 如：a,b,c都在“1”键上，输入a只需要按一次，输入c需要连续按三次。 如果连续两个字符不在同一个按键上，则可直接按，如：ad需要按两下，kz需要按6下 如果连续两字符在同一个按键上，则两个按键之间需要等一段时间，如ac，在按了a之后，需要等一会儿才能按c。 现在假设每按一次需要花费一个时间段，等待时间需要花费两个时间段。 现在给出一串字符，需要计算出它所需要花费的时间。

#### 输入描述

> ```c++
> 一个长度不大于100的字符串，其中只有手机按键上有的小写字母
> ```

#### 输出描述

> ```c++
> 输入可能包括多组数据，对于每组数据，输出按出Input所给字符串所需要的时间
> ```

### 示例

输入：

```c++
bob
www
```

输出：

```c++
7
7
```

### 思路

先贴一下 26 个字母的分布：

|      | ABC  | DEF  |
| ---- | ---- | ---- |
| GHI  | JKL  | MNO  |
| PQRS | TUV  | WXYZ |

规则很清晰，就是字母在哪一块的第几个位置就按几下，相邻的字母如果在同一块上面就需要等待 2 个时间段，所以我们需要做的第一步其实是应该存一下每个字母所在的位置，然后就很容易求了。

```c++
#include<iostream>
#include<vector>

using namespace std;

class Block{
public:
    int block;
    int pos;
public:
    Block(int block, int pos) : block(block), pos(pos){}
};

int getCost(string s, vector<Block>& chars){
    int cnt = 0, n = s.size();
    for(int i = 0; i < n; i ++){
        cnt += chars[s[i] - 'a'].pos;
        if(i > 0 && chars[s[i] - 'a'].block == chars[s[i - 1] - 'a'].block) 
            cnt += 2;
    }
    return cnt;
}

int main(){
    string s;
    vector<Block> chars;
    // 初始化字母的位置
    for(int i = 0; i < 18; i ++)
        chars.emplace_back(i / 3, i % 3 + 1);
    chars.emplace_back(5, 4); chars.emplace_back(6, 1);
    chars.emplace_back(6, 2); chars.emplace_back(6, 3);
    chars.emplace_back(7, 1); chars.emplace_back(7, 2);
    chars.emplace_back(7, 3); chars.emplace_back(7, 4);
    while(cin >> s){
        cout << getCost(s, chars) << endl;
    }
    return 0;
}
```

更简单的做法，这个就不用存每个字母的位置了，因为如果两个字母在一个按钮里面，那个 pos 肯定是连续的，所以字母的距离和 pos 之差应该相等。

```c++
#include<iostream>
#include<string>
using namespace std;
int main(){
    int key[26] = {1,2,3,1,2,3,1,2,3,1,2,3,1,2,3,1,2,3,4,1,2,3,1,2,3,4};
    string str;
    while(cin >> str){
        int count = key[str[0]-'a'];
        for(int i = 1; i < str.size(); i ++){
            count += key[str[i]-'a'];
            if(key[str[i]-'a']-key[str[i-1]-'a'] == str[i]-str[i-1])//判断是否在同一个按键上
                count+=2;
        }
        cout << count << endl;
    }
    return 0;
}
```

