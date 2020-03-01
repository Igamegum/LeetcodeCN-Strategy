# Problem
[Link](https://leetcode-cn.com/problems/linked-list-in-binary-tree/)

# Solution

* 枚举树上的起点，然后遍历即可
* 时间复杂度O(n*n)

# Code
```cpp
class Solution {
public:
    bool is_same(ListNode* head,  TreeNode* root) {
        if (head == NULL) return true;
        if (root == NULL && head != NULL) return false;
        if (root->val != head->val) return false;
        bool lhs_res = is_same(head->next, root->left);
        bool rhs_res = is_same(head->next, root->right);
        return lhs_res || rhs_res;
    }
    
    std::vector<TreeNode *> nodes;
    
    void dfs(TreeNode* root) {
        if (root == NULL) return;
        nodes.push_back(root);
        dfs(root->left);
        dfs(root->right);
    }
    
    bool isSubPath(ListNode* head, TreeNode* root) {
        nodes.clear();
        dfs(root);
        for (int i = 0; i < nodes.size(); ++i) {
            if (is_same(head, nodes[i])) {
                return true;
            }
        }
        return false;
    }
};
```