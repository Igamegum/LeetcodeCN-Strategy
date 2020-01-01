# Problem
[Link](https://leetcode-cn.com/problems/deepest-leaves-sum/)

# Solution

* 直接遍历即可，维护最大层数和对应的叶子节点的和
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    
    int ans;
    int deep;
    void dfs(TreeNode* root,  int de)
    {   
        if (root->left == NULL && root->right == NULL) {
            if (de == deep) ans += root->val;
            else if (de > deep) deep = de, ans = root->val;
            return ;
        }
        if (root->left)  dfs(root->left,  de + 1);
        if (root->right) dfs(root->right, de + 1);        
    }
    int deepestLeavesSum(TreeNode* root) {
        ans  = 0;
        deep = 0;
        if (root == NULL) return 0;
        dfs(root, 0);
        return ans;
    }
};
```