# Problem
[Link](https://leetcode-cn.com/problems/balance-a-binary-search-tree/)

# Solution

* 先遍历原树，将元素排序，然后递归建立二叉树即可
* 时间复杂度O(n * logn)

# Code
```cpp
class Solution {
public:
    std::vector<int> values;
    void dfs(TreeNode* root) {
        if (root == NULL) return;
        values.push_back(root->val);
        dfs(root->left);
        dfs(root->right);
    }
    TreeNode* build(int L, int R) {
        if (R < L || L < 0 || R >= values.size())  return NULL;
        int mid = (L + R) >> 1;
        TreeNode *  root = new TreeNode(values[mid]);
        root->left = build(L, mid - 1);
        root->right = build(mid + 1, R);
        return root;
    }
    TreeNode* balanceBST(TreeNode* root) {
        values.clear();
        dfs(root);
        std::sort(values.begin(), values.end());
        return build(0, values.size() - 1);
    }
};
```