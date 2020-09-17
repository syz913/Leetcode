### 题目描述

有一个同学在学习分式。他需要将一个连分数化成最简分数，你能帮助他吗？

<img src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/09/09/fraction_example_1.jpg" alt="img" style="zoom:50%;" />

连分数是形如上图的分式。在本题中，所有系数都是大于等于0的整数。

 

输入的`cont`代表连分数的系数（`cont[0]`代表上图的`a0`，以此类推）。返回一个长度为2的数组`[n, m]`，使得连分数的值等于`n / m`，且`n, m`最大公约数为1。

### 示例

**示例 1：**

```C++
输入：cont = [3, 2, 0, 2]
输出：[13, 4]
解释：原连分数等价于3 + (1 / (2 + (1 / (0 + 1 / 2))))。注意[26, 8], [-13, -4]都不是正确答案。
```

**示例 2：**

```C++
输入：cont = [0, 0, 3]
输出：[3, 1]
解释：如果答案是整数，令分母为1即可。
```

### 思路

直接递归好了，如果 [1, n] 部分的值为 $n_1/m_1$

那么 $cont[0] + n_1/m_1 =(cont[0]*m_1 + n_1)/m_1$

```C++
class Solution {
public:
    vector<int> fraction(vector<int>& cont) {
        if (cont.size() == 1)
            return { cont[0],1 };
        vector<int>b(cont.begin()+1, cont.end());
        vector<int> t = fraction(b);
        return {cont[0]*t[0]+t[1],t[0]};
    }
};
```

