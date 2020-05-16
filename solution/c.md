# Problem
[Link]()

# Solution
* 直接DFS
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int dfs(TreeNode * root, int premax) {
        if (root == NULL) return 0;
        int ans = 0;
        if (premax <= root->val) ++ans;
        ans += dfs(root->left, std::max(premax, root->val));
        ans += dfs(root->right, std::max(premax, root->val));
        return ans;
    }
    int goodNodes(TreeNode* root) {
        return dfs(root, -0x3f3f3f3f);
    }
};
```