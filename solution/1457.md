# Problem
[Link](https://leetcode-cn.com/problems/pseudo-palindromic-paths-in-a-binary-tree/)

# Solution
* 直接模拟,关键在于判断N个数字能否组成会回文串，只要出现次数为奇数的数字个数小于等于1，那么这些数字一定能组成回文串
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    std::map<int, int> mp;
    bool check() {
        int odd = 0;
        for (auto it = mp.begin(); it != mp.end(); ++it) {
            if (it->second & 1) ++odd;
        }
        return odd <= 1;
    }
    
    int dfs(TreeNode* root) {
        if (root == NULL) return 0;
        ++mp[root->val];
        if (root->left == NULL && root->right == NULL) {
            bool res = check();
            --mp[root->val];
            return res ? 1 : 0;        
        }
        int lhs = dfs(root->left);
        int rhs = dfs(root->right);
        --mp[root->val];
        return lhs + rhs;
        
    }
    int pseudoPalindromicPaths (TreeNode* root) {
        mp.clear();
        return dfs(root);
    }
};
```