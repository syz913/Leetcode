> 题目描述：给定一个二叉树，判断它是否对称

eg:

```java
For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3
 

But the following [1,2,2,null,3,null,3] is not:

    1
   / \
  2   2
   \   \
   3    3

```

> 思路描述：直观的可以看出来中序遍历对称，但是特殊情况会导致错误，[1,2,2,2,null,2]
>
> 所以要考虑左子树和右子树不同时为空的情况。简单粗暴的左右比较也可以。

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool check(TreeNode* p1,TreeNode* p2){
        if(!p1 && !p2)
            return true;
        else if(!p1||!p2) 
            return false;
        return (p1->val == p2->val && check(p1->left, p2->right) && check(p1->right, p2->left));
    }
    
    bool isSymmetric(TreeNode* root) {
        if(!root)
            return true;
        if(check(root,root))
            return true;
        else return false;
    }
};
```
