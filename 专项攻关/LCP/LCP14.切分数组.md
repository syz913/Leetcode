### 题目描述

给定一个整数数组 `nums` ，小李想将 `nums` 切割成若干个非空子数组，使得每个子数组最左边的数和最右边的数的最大公约数大于 1 。为了减少他的工作量，请求出最少可以切成多少个子数组。

### 示例

**示例 1：**

> 输入：`nums = [2,3,3,2,3,3]`
>
> 输出：`2`
>
> 解释：最优切割为 [2,3,3,2] 和 [3,3] 。第一个子数组头尾数字的最大公约数为 2 ，第二个子数组头尾数字的最大公约数为 3 。

**示例 2：**

> 输入：`nums = [2,3,5,7]`
>
> 输出：`4`
>
> 解释：只有一种可行的切割：[2], [3], [5], [7]

### 思路

最简单的思路就是找到和左节点 gcd > 1 的数，作为右节点进行递归寻找其中的最小值，这个容易想到

但是会超时

```C++
class Solution {
public:
    int minSplit(vector<int>& nums, int idx, int n){
        if(idx >= n) return 0;
        if(n - idx == 1) return 1;
        int minAns = n;
        for(int i = idx + 1; i < n; i ++){
            if(__gcd(nums[idx], nums[i]) > 1){
                minAns = min(minAns, minSplit(nums, i + 1, n) + 1);
            }
        }
        minAns = min(minAns, minSplit(nums, idx + 1, n) + 1);
        return minAns;
    }
    int splitArray(vector<int>& nums) {
        int n = nums.size();
        return minSplit(nums, 0, n);
    }
};
```

其实我们上面的方案已经很好了，但是时间复杂度为 $O(n^2)$，稍微有点大，我们看一下计算过程，对于每一个

```C++
const int N = 1e6 + 10;

int f[N],minv[N];

class Solution {
public:
    int n;
    int splitArray(vector<int>& nums) {
        memset(f,0,sizeof f);
        memset(minv,0x3f,sizeof minv);

        n = nums.size();

        for(int i=1;i<=n;i++){
            int x = nums[i - 1];
            f[i] = f[i - 1] + 1;
            for(int j = 2; j * j <= x; j ++ ){
                if(x % j == 0){
                    f[i] = min(f[i],minv[j] + 1);
                    minv[j] = min(minv[j],f[i - 1]);
                    while(x % j == 0) x = x / j;
                }
            }
            if(x > 1) {
                f[i] = min(f[i],minv[x] + 1);
                minv[x] = min(minv[x],f[i - 1]);
            }

        }
        return f[n];
    }
};
```

