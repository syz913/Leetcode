### 题目描述

 每年毕业的季节都会有大量毕业生发起狂欢，好朋友们相约吃散伙饭，网络上称为“bg”。参加不同团体的bg会有不同的感觉，我们可以用一个非负整数为每个bg定义一个“快乐度”。现给定一个bg列表，上面列出每个bg的快乐度、持续长度、bg发起人的离校时间，请你安排一系列bg的时间使得自己可以获得最大的快乐度。   例如有4场bg：   第1场快乐度为5，持续1小时，发起人必须在1小时后离开；   第2场快乐度为10，持续2小时，发起人必须在3小时后离开；   第3场快乐度为6，持续1小时，发起人必须在2小时后离开；   第4场快乐度为3，持续1小时，发起人必须在1小时后离开。   则获得最大快乐度的安排应该是：先开始第3场，获得快乐度6，在第1小时结束，发起人也来得及离开；再开始第2场，获得快乐度10，在第3小时结束，发起人正好来得及离开。此时已经无法再安排其他的bg，因为发起人都已经离开了学校。因此获得的最大快乐度为16。   注意bg必须在发起人离开前结束，你不可以中途离开一场bg，也不可以中途加入一场bg。 又因为你的人缘太好，可能有多达30个团体bg你，所以你需要写个程序来解决这个时间安排的问题。

#### 输入描述　　

> ```c++
> 测试输入包含若干测试用例。每个测试用例的第1行包含一个整数N (<=30)，随后有N行，每行给出一场bg的信息：
>     h l t
>     其中 h 是快乐度，l是持续时间（小时），t是发起人离校时间。数据保证l不大于t,因为若发起人必须在t小时后离开，bg必须在主人离开前结束。
> 
>     当N为负数时输入结束。
> ```

#### 输出描述

> ```c++
> 每个测试用例的输出占一行，输出最大快乐度。
> ```

### 示例

输入：

```c++
3
6 3 3
3 2 2
4 1 3
4
5 1 1
10 2 3
6 1 2
3 1 1
-1
```

输出：

```c++
7
16
```

### 思路

背包思想，我们用 dp\[i][j] 表示前 i 个 bg 在时间 j 内可以获得的最大快乐度，那么最后要求的就是 n 个 bg 在 maxTime 时间内可以获得的最大快乐度，可以选择参加第 i 个 bg 或者不参加第 i 个 bg，得到以下状态转移方程：

$dp[i,j]=max\{dp[i-1,j],dp[i-1,j-bg[i].time] + bg[i].happy\}$

```c++
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;

struct Bg{
    int happy, time, endTime;
    Bg(int h, int l, int t) : happy(h), time(l), endTime(t){}
    
    bool operator < (const Bg& bg) const {
        return endTime < bg.endTime || (endTime == bg.endTime && time <= bg.time);
    }
};
int main(){
    int n;
    while(cin >> n && n > 0){
        int h, l, t;
        int maxtime = 0;
        vector<Bg> bg;
        for(int i = 0; i < n; i ++){
            cin >> h >> l >> t;
            maxtime = max(maxtime, t);
            bg.emplace_back(h, l, t);
        }
        sort(bg.begin(), bg.end());
        vector<vector<int>> dp(n, vector<int>(maxtime + 1, 0));
        for(int i = 0; i < n; i ++){
            for(int j = bg[i].time; j <= bg[i].endTime; j ++){
                if(i == 0) dp[i][j] = bg[i].happy;
                else dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - bg[i].time] + bg[i].happy);
            }
        }          
        cout << dp[n - 1][maxtime] << endl;
    }
}
```

优化空间复杂度

```c++
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;

struct Bg{
    int happy, time, endTime;
    Bg(int h, int l, int t) : happy(h), time(l), endTime(t){}
    
    bool operator < (const Bg& bg) const {
        return endTime < bg.endTime;
    }
};
int main(){
    int n;
    while(cin >> n && n > 0){
        int h, l, t;
        int maxtime = 0;
        vector<Bg> bg;
        for(int i = 0; i < n; i ++){
            cin >> h >> l >> t;
            maxtime = max(maxtime, t);
            bg.emplace_back(h, l, t);
        }
        sort(bg.begin(), bg.end());
        vector<int> dp(maxtime + 1, 0);
        int ans = 0;
        for(int i = 0; i < n; i ++){
            for(int j = bg[i].endTime; j >= bg[i].time; j --){
                dp[j] = max(dp[j], dp[j - bg[i].time] + bg[i].happy);
                ans = max(ans, dp[j]);
            }
        }
        cout << ans << endl;
    }
}
```

