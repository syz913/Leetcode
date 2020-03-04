> 题目描述：给定一个二叉搜索树，根节点为node。返回任意两个结点值的相差最小值。

eg:

```java
Example :

Input: root = [4,2,6,1,3,null,null]
Output: 1
Explanation:
Note that root is a TreeNode object, not an array.

The given tree [4,2,6,1,3,null,null] is represented by the following diagram:

          4
        /   \
      2      6
     / \    
    1   3  

while the minimum difference in this tree is 1, it occurs between node 1 and node 2, also between node 3 and node 2.
```

> 思路描述：进行中序遍历，二叉搜索树是有序的。
>
> 前序遍历：根结点 ---> 左子树 ---> 右子树
>
> 中序遍历：左子树---> 根结点 ---> 右子树
>
> 后序遍历：左子树 ---> 右子树 ---> 根结点

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
    int ret = INT_MAX, pre_value = -1;
    bool first = true;
    
    int minDiffInBST(TreeNode* root) {
        if (root->left) {
            minDiffInBST(root->left);
        }
        if (first) {
            first = !first;
            pre_value = root->val;
        } else {
            ret = min(ret, root->val - pre_value);
            pre_value = root->val;
        }
        if (root->right) {
            minDiffInBST(root->right);
        }
        return ret;
    }
};
```

