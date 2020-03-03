> 题目描述：和96题类似，只不过输出的不是二叉搜索树的数目，而是二叉搜索树前序遍历。

eg:

```java
Example:

Input: 3
Output:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
Explanation:
The above output corresponds to the 5 unique BST's shown below:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

> 思路描述：
>
> 1. 根节点可以任取min ~ max (例如min  = 1, max = n)，假如取定为i。
>
> 2. 则left subtree由min ~ i-1组成，假设可以有L种可能。right subtree由i+1 ~ max组成，假设有R种可能。生成所有可能的left/right subtree。
>
> 3. 对于每个生成的left subtree/right subtree组合，p = 1...L，q = 1...R，添加上根节点i而组成一颗新树。

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
    vector<TreeNode *> generateTrees(int n) {
        vector<TreeNode *> ret;
        if(n == 0)
            return ret;
        return genBST(1, n);
    }
    
    vector<TreeNode *> genBST(int min, int max) {
        vector<TreeNode *> ret;
        if(min > max) {
            ret.push_back(NULL);
            return ret;
        }
        for(int i = min; i <= max; i ++) {
            vector<TreeNode*> leftSubTree = genBST(min, i - 1);
            vector<TreeNode*> rightSubTree = genBST(i + 1, max);
            for(int j = 0; j < leftSubTree.size(); j ++) {
                for(int k = 0; k < rightSubTree.size(); k ++) {
                    TreeNode *root = new TreeNode(i);
                    root->left = leftSubTree[j];
                    root->right = rightSubTree[k];
                    ret.push_back(root);
                }
            }
        }
        return ret;
    }
};
```
