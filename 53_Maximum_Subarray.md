> 题目描述：给定一个整数数组nums，找到有最大和的相邻子串然后返回和。

eg:

```java
Example:

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

> 思路描述：比如-2，1，-3，4，-1，最大值是-1+4，因为4前面最大的的子串就是4了，只要依次找到[0,i]的最大子串即可。

```C++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        int sum = nums[0], ans = sum;
        for(int i = 1; i < n; i ++){
            sum = max(nums[i], sum + nums[i]);//找到[0, i]的最大和
            if(sum > ans)
                ans = sum;
        }
        return ans;
    }
};
```
