### 题目描述

在战略游戏中，玩家往往需要发展自己的势力来触发各种新的剧情。一个势力的主要属性有三种，分别是文明等级（`C`），资源储备（`R`）以及人口数量（`H`）。在游戏开始时（第 0 天），三种属性的值均为 0。

随着游戏进程的进行，每一天玩家的三种属性都会对应**增加**，我们用一个二维数组 `increase` 来表示每天的增加情况。这个二维数组的每个元素是一个长度为 3 的一维数组，例如 `[[1,2,1],[3,4,2]]` 表示第一天三种属性分别增加 `1,2,1` 而第二天分别增加 `3,4,2`。

所有剧情的触发条件也用一个二维数组 `requirements` 表示。这个二维数组的每个元素是一个长度为 3 的一维数组，对于某个剧情的触发条件 `c[i], r[i], h[i]`，如果当前 `C >= c[i]` 且 `R >= r[i]` 且 `H >= h[i]` ，则剧情会被触发。

根据所给信息，请计算每个剧情的触发时间，并以一个数组返回。如果某个剧情不会被触发，则该剧情对应的触发时间为 -1 。

### 示例

**示例 1：**

> 输入： `increase = [[2,8,4],[2,5,0],[10,9,8]]` `requirements = [[2,11,3],[15,10,7],[9,17,12],[8,1,14]]`
>
> 输出: `[2,-1,3,-1]`
>
> 解释：
>
> 初始时，C = 0，R = 0，H = 0
>
> 第 1 天，C = 2，R = 8，H = 4
>
> 第 2 天，C = 4，R = 13，H = 4，此时触发剧情 0
>
> 第 3 天，C = 14，R = 22，H = 12，此时触发剧情 2
>
> 剧情 1 和 3 无法触发。

**示例 2：**

> 输入： `increase = [[0,4,5],[4,8,8],[8,6,1],[10,10,0]]` `requirements = [[12,11,16],[20,2,6],[9,2,6],[10,18,3],[8,14,9]]`
>
> 输出: `[-1,4,3,3,3]`

**示例 3：**

> 输入： `increase = [[1,1,1]]` `requirements = [[0,0,0]]`
>
> 输出: `[0]`

### 思路

最简单的思路就是遍历，每天增加属性值之后去判断是否会触发新的剧情

但是会超时

```C++
class Solution {
public:
    vector<int> getTriggerTime(vector<vector<int>>& increase, vector<vector<int>>& requirements) {
        int nums[3] = {0};
        int m = increase.size(), n = requirements.size();
        vector<int> ans(n, -1);
        for(int i = 0; i < m; i ++){
            vector<int> in = increase[i];
            nums[0] += in[0], nums[1] += in[1], nums[2] += in[2];
            for(int j = 0; j < n; j ++){
                vector<int> requirement = requirements[j];
                if(requirement[0] == 0 && requirement[1] == 0 && requirement[2] == 0) ans[j] = 0;
                else if(ans[j] == -1 && requirement[0] <= nums[0] && requirement[1] <= nums[1] && requirement[2] <= nums[2]){
                    ans[j] = i + 1;
                }
            }
        }
        return ans;
    }
};
```

换一种想法，本质上都是一样的，如果我们用一个数组存储了每一天每个属性的值，比如用 nums[i\][j] 表示第 i 天第 j 种属性的值，那么我们想要寻找在哪一天触发一个剧情，应该怎么办呢？

触发剧情需要满足三个属性都得小于等于 nums[i\][0]、nums[i\][1]、nums[i\][2]

我们注意到 nums[i] 一定是递增的，因为下一天三个属性一定比前一天要高，这里把一个 vector 当成一个元素来看了，其实没啥区别。那我们就可以使用二分法了。

```C++
class Solution {
public:
    vector<int> getTriggerTime(vector<vector<int>>& increase, vector<vector<int>>& requirements) {
        int m = increase.size();
        vector<vector<int>> nums(m, vector<int>(3, 0));
        for(int i = 0; i < m; i ++){
            for(int j = 0; j < 3; j ++){
                if(i == 0) nums[i][j] = increase[i][j];
                else nums[i][j] = nums[i - 1][j] + increase[i][j];
            }
        }
        vector<int> ans;
        for(auto v : requirements){
            if(v[0] == 0 && v[1] == 0 && v[2] == 0){
                ans.push_back(0); continue;
            }
            int l = 0, r = m - 1;
            while(l < r){
                int mid = (l + r) / 2;
                if(nums[mid][0] >= v[0] && nums[mid][1] >= v[1] && nums[mid][2] >= v[2])
                    r = mid;
                else
                    l = mid + 1;
            }
            if(nums[l][0] >= v[0] && nums[l][1] >= v[1] && nums[l][2] >= v[2])
                ans.push_back(l + 1);
            else
                ans.push_back(-1);
        }
        return ans;
    }
};
```

