
# Problem
[Link](https://leetcode-cn.com/problems/all-elements-in-two-binary-search-trees/)

# Solution

* 遍历二叉树，将数字放到容器中，然后排序即可。
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    std::multiset<int> S;
    void dfs(TreeNode* root) {
        if (root == NULL) return;
        S.insert(root->val);
        dfs(root->left);
        dfs(root->right);
    }
    vector<int> getAllElements(TreeNode* root1, TreeNode* root2) {
        S.clear();
        dfs(root1);
        dfs(root2);
        std::vector<int> ans;
        for (auto it = S.begin(); it != S.end(); ++it) {
            ans.push_back(*it);
        }
        return ans;
    }
};
```
