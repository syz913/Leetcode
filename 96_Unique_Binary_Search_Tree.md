> 题目描述：给定n，求由1...n组成的二叉搜索树有多少种。

eg:

```java
Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

> 思路描述：这一题主要是考察二叉搜索树的特征，左小右大。
>
> 如果1或n为树根，那么下面就相当于n-1个数构成的二叉搜索树；
>
> 若k为树根，那么左子树相当于k - 1个数构成的二叉搜索树，右子树相当于n - k个数构成的二叉搜索树。
>
> a[n] = 2a[n-1] + a[1]\*a[n-2] + a[2]\*a[n-3] + a[3]\*a[n-4] + ..... + a[n-2]\*a[1]，
>
> 若令a[0] = 1,
>
> 则a[n] = a[0]\*a[n-1] + a[1]\*a[n-2] + a[2]\*a[n-3] + a[3]\*a[n-4] + ..... + a[n-2]\*a[1] + a[n-1]\*a[0]，
>
> 所以简单粗暴的递归即可。

```C++
class Solution {
public:
    int numTrees(int n) {
        if(n == 1)
            return 1;
        if(n == 2)
            return 2;
        int sum = 2*numTrees(n-1);
        for(int i = 1; i < n - 1; i ++)
            sum += numTrees(i)*numTrees(n - i - 1);
        return sum;
    }
};
```

但是时间复杂度太高，明显可以进行优化，其实思路也是上面的思路，这告诉我们，能不用递归尽量进行转换。

```C++
class Solution {
public:
    int numTrees(int n) {
        vector<int> a(n + 1, 0);
        a[0] = 1;
        for(int i = 1; i < n + 1; i ++)
            for(int j = 0; j < i; j ++)
                a[i] += a[j]*a[i - j -1];
        return a[n];
    }
};
```
