# Problem
[Link](https://leetcode-cn.com/problems/maximum-product-of-splitted-binary-tree/)

# Solution

* 分裂后，必定是某棵子树和剩余的部分，所以只需要记录整棵树的元素和再枚举子树即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:

    const int mod = 1e9 + 7;
    std::vector<int> values;
    int dfs(TreeNode* root) {
        if (root == NULL) return 0;
        int lhs = dfs(root->left);
        int rhs = dfs(root->right);
        values.push_back(lhs + rhs + root->val);
        return lhs + rhs + root->val;
    }


    int maxProduct(TreeNode* root) {
        values.clear();
        int sum = dfs(root);
      
        long long ans = 0;
        for (int i = 0; i < values.size(); ++i) {
            ans = std::max(ans, (long long )values[i] * (sum - values[i]));
        }
        ans %= mod;
        return ans;
    }
};
```