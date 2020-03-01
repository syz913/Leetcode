> 题目描述：给定一个三角形，找出从上到下的最小路径和。每一步都可以移动到下面一行的相邻数字。

eg:

```java
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is `11` (i.e., **2** + **3** + **5** + **1** = 11).

> 思路描述：直观思路是递归，逐层递归即可，好点的思路是动态规划，比较容易理解，就不过多叙述

```C++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        for(int i = n - 1; i > 0; i --) {
            for(int j = 0; j < i; j ++) {
                triangle[i-1][j] += min(triangle[i][j], triangle[i][j+1]);
            }
        }
        return triangle[0][0];                           
    }
};
```

类似的一维解法

```C++
    int minimumTotal(vector<vector<int>>& triangle) {
        if(triangle.empty()){
            return 0;
        }
        int m = triangle.size();
        vector<int> dp(m);
        for(int i = 0; i < m; i++){
            dp[i] = triangle[m-1][i]; 
        }
        for(int i = m-2; i >=0; i--){
            for(int j = 0; j <= i; j++){
                dp[j]= min(triangle[i][j]+dp[j], triangle[i][j]+dp[j+1]);               
            }
        }
        return dp[0];
    }
```



超时的递归

```C++
int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        if(n == 0)
            return 0;
        if(n == 1)
            return triangle[0][0];
        if(n == 2)
            return triangle[0][0] + min(triangle[1][0], triangle[1][1]);
        vector<vector<int>> left, right;
        for(int i = 1; i < n; i ++){
            vector<int> vec(i,0);
            for(int j = 0; j < i; j ++){
                vec[j] = triangle[i][j];
            }
            left.push_back(vec);
        }
        for(int i = 1; i < n; i ++){
            vector<int> vec(i,0);
            for(int j = 1; j < i + 1; j ++){
                vec[j - 1] = triangle[i][j];
            }
            right.push_back(vec);
        }
        return triangle[0][0] + min(minimumTotal(left), minimumTotal(right));
    }
```

