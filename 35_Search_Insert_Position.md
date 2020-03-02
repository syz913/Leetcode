> 题目描述：给定一个排好序的数组（假定不重复）以及一个数字，返回它的位置或者可以被插入的位置下标。

eg:

```java
Example 1:

Input: [1,3,5,6], 5
Output: 2
Example 2:

Input: [1,3,5,6], 2
Output: 1
Example 3:

Input: [1,3,5,6], 7
Output: 4
Example 4:

Input: [1,3,5,6], 0
Output: 0
```

> 思路描述：easy难度的一道题，这个就很清晰了，找到大于等于它的数下标即可。

```C++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int n = nums.size();
        if(n == 0)
            return 0;
        for(int i = 0; i < n; i ++)
            if(nums[i] >= target)
                return i;
        return n;
    }
};
```
