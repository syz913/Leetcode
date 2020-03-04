> 题目描述：给定一个两个有序整数数组，合并。

```java
Example:

Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

> 思路描述：合并有序数组

```C++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int count = m;
        if(m == 0){
            for(int j = 0; j < n; j ++){
                nums1[j] = nums2[j];
            }
            return;
        }
        if(n == 0)
            return;
        if(nums1[m - 1] <= nums2[0])
            for(int i = m; i < m + n; i ++)
                nums1[i] = nums2[i - m];
        else if(nums1[0] >= nums2[n - 1]){
            for(int i = n; i < m + n; i ++)
                nums1[i] = nums1[i - n];
            for(int i = 0; i < n; i ++)
                nums1[i] = nums2[i];
        }
        else 
            for(int j = 0; j < n; j ++){
                for(int i = count - 1; i >= 0; i --){
                    if(nums2[j] >= nums1[i]){
                        nums1[i + 1] = nums2[j];
                        count ++;
                        break;
                    }
                    nums1[i + 1] = nums1[i];
                    if(i == 0){
                        nums1[i] = nums2[j];
                        count ++;
                    }
                }   
            }
    }
};
```

