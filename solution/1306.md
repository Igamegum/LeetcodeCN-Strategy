
# Problem
[Link](https://leetcode-cn.com/problems/jump-game-iii/)

# Solution

* 在一个节点上，存在往左跳或者往右跳的选择，直接搜索即可，由于每个节点只能访问一次，所以总的状态数不超过n
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    std::vector<bool> vis;
    bool dfs(const vector<int>& arr, int id) {
        if (arr[id] == 0) return true;
        bool res = false;
        
        if (id + arr[id] < arr.size() && vis[id + arr[id]] == false) {
            vis[id + arr[id]] = true;
            res = dfs(arr, id + arr[id]);
            vis[id + arr[id]] = false;
            if (res) return true;
        }
        
        if (id - arr[id] >= 0 && vis[id - arr[id]] == false) {
            vis[id - arr[id]] = true;
            res = dfs(arr, id - arr[id]);
            vis[id - arr[id]] = false;
            if (res) return true;
        }
        
        return false;
    }
    bool canReach(vector<int>& arr, int start) {
        vis = std::vector<bool>(arr.size(), false);
        vis[start] = true;
        bool ans = dfs(arr, start);
        return ans;
    }
};
```