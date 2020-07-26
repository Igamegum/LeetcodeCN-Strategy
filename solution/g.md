
# Problem
[Link]()

# Solution
* 直接暴力记录每一层的叶子节点的高度，然后分别枚举左子树的叶子节点和右子树的叶子节点，两个叶子节点之间的距离等于两者的高度和减去两倍的当前节点的高度
* 时间复杂度：O(n*n*n)

# Code
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int ans;
    std::vector<int> dfs(TreeNode* root, int deep, const int dist) {
        if (root == NULL) return {};
        if (root->left == NULL && root->right == NULL) {
            return {deep};
        }
        std::vector<int> lhs = dfs(root->left, deep + 1, dist);
        std::vector<int> rhs = dfs(root->right, deep + 1, dist);
        
        std::sort(lhs.begin(), lhs.end());
        std::sort(rhs.begin(), rhs.end());
        for (int i = 0; i < lhs.size(); ++i) {
            if (lhs[i] - 2 * deep > dist) break;
            for (int j = 0; j < rhs.size(); ++j) {
                int sum = lhs[i] + rhs[j] - 2 * deep;
                if (sum > dist) break;
                if (sum <= dist) ++ans;
            }
        }
        
        for (int i = 0; i < rhs.size(); ++i) {
            lhs.push_back(rhs[i]);
        }
        return lhs;
    }
    int countPairs(TreeNode* root, int distance) {
        ans = 0;
        dfs(root, 0, distance);
        return ans;
    }
};
```