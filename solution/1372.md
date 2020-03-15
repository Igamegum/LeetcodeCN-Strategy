# Problem
[Link](https://leetcode-cn.com/problems/longest-zigzag-path-in-a-binary-tree/)

# Solution

* 对于一个节点，分别维护其往左上方走和往右上方走的最长交错路径的节点数，其中往左上方走的路径的节点数我们用L表示，同理，往右上方的用R表示，实际上我们在维护一个二元组(L,R)。
* 如果一个节点是空节点，显然返回(0,0)这个二元组。
* 如果一个节点不为空节点，那么 L = 左孩子的R + 1， R = 右孩子的L + 1。
* 遍历二叉树，自底向上维护即可。
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int L_max;
    int R_max;
    std::pair<int, int> dfs(TreeNode *root) {
        if (root == NULL) return std::make_pair(0, 0);
        std::pair<int, int> lhs = dfs(root->left);
        std::pair<int, int> rhs = dfs(root->right);
        int rr = rhs.first + 1;
        int ll = lhs.second + 1;
        L_max = std::max(ll, L_max);
        R_max = std::max(rr, R_max);
        return std::make_pair(ll, rr);
    }
    
    int longestZigZag(TreeNode* root) {
        L_max = 1;
        R_max = 1;
        dfs(root);
        return std::max(L_max - 1, R_max - 1);
    }
};
```