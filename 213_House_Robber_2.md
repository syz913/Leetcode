> 题目描述：盗贼问题，有一串围成圆的房子可以被盗，同时相邻房间有防盗系统即一晚上不能同时盗相邻房间，求一晚上可以盗的最多钱数。

eg:

```java
Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.
                 
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

> 思路描述：这道题和house robber的区别是首尾成环了，并且我们可以注意到第一间房和最后一间房不能够同时偷，所以可以求分别不偷第一间房和最后一间房的最大值，然后解法就和house robber 一样了。对于这类求极值的问题首先考虑动态规划 Dynamic Programming 来解，维护一个一位数组 dp，其中 dp[i] 表示 [0, i] 区间可以抢夺的最大值，对当前i来说，有抢和不抢两种互斥的选择，不抢即为 dp[i-1]（等价于去掉 nums[i] 只抢 [0, i-1] 区间最大值），抢即为 dp[i-2] + nums[i]（等价于去掉 nums[i-1]）。再举一个简单的例子来说明一下吧，比如说 nums为{3, 2, 1, 5}，那么来看 dp 数组应该是什么样的，首先 dp[0]=3 没啥疑问，再看 dp[1] 是多少呢，由于3比2大，所以抢第一个房子的3，当前房子的2不抢，则dp[1]=3，那么再来看 dp[2]，由于不能抢相邻的，所以可以用再前面的一个的 dp 值加上当前的房间值，和当前房间的前面一个 dp 值比较，取较大值当做当前 dp 值，这样就可以得到状态转移方程 dp[i] = max(num[i] + dp[i - 2], dp[i - 1]), 且需要初始化 dp[0] 和 dp[1]，其中 dp[0] 即为 num[0]，dp[1] 此时应该为 max(num[0], num[1])

```C++
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 0)
            return 0;
        else if(n == 1)
            return nums[0];
        else if(n == 2)
            return max(nums[0], nums[1]);
        vector<int> dp1, dp2;
        dp1.insert(dp1.begin(), nums.begin(), nums.end() - 1);
        dp2.insert(dp2.begin(), nums.begin() + 1, nums.end());
        return max(robber(dp1), robber(dp2));
    }
    
    int robber(vector<int>& nums) {
        vector<int> dp = {nums[0], max(nums[0], nums[1])};
        for (int i = 2; i < nums.size(); ++i) {
            dp.push_back(max(nums[i] + dp[i - 2], dp[i - 1]));
        }
        return dp.back();
    }
};
```

