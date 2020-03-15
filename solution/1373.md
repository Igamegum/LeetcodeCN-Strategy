# Problem
[Link](https://leetcode-cn.com/problems/maximum-sum-bst-in-binary-tree/)

# Solution
* 对于一个节点，如果其左孩子是二叉搜索树，右孩子也是二叉搜索树，且当前节点的值大于左孩子，小于右孩子，那么以这个节点为根的子树也是二叉搜索树。
* 遍历二叉树，自底向上维护即可。
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int ans = 0;
    std::pair<bool, int> dfs(TreeNode* root) {
        if (root == NULL) return std::make_pair(true, 0);
        std::pair<bool, int> lhs = dfs(root->left);
        std::pair<bool, int> rhs = dfs(root->right);
        int sum = lhs.second + rhs.second + root->val;
        bool is = false;
        if (lhs.first 
            && rhs.first 
            && ((root->left  != NULL && root->val > root->left->val)   || (root->left == NULL)) 
            && ((root->right != NULL && root->val < root->right->val) || (root->right == NULL))) {
            is = true;
        }
        if (is) ans = std::max(ans, sum);
        return std::make_pair(is, sum);
    }
    int maxSumBST(TreeNode* root) {
        ans = 0;
        dfs(root);
        return ans;
    }
};

```