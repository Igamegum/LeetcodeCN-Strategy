# Problem
[Link](https://leetcode-cn.com/problems/chuan-di-xin-xi/)

# Solution

* 建图，然后直接搜索遍历，最多搜索k层即可
* 时间复杂度O(n * k)

# Code
```cpp
class Solution {
public:
    int ans = 0;
    std::vector< std::vector<int> > edge;
    
    void dfs(int id, int ceil, const int k, const int n) {
        if (id == n - 1 && ceil == k) {
            ++ans;
            return;
        }
        if (ceil >= k) return;
        
        for (int i = 0; i < edge[id].size(); ++i) {
            dfs(edge[id][i], ceil + 1, k, n);
        }
    }
    int numWays(int n, vector<vector<int>>& relation, int k) {
        edge.clear();
        edge = std::vector< std::vector<int> > (n, std::vector<int>());
        
        for (int i = 0; i < relation.size(); ++i) {
            int a = relation[i][0];
            int b = relation[i][1];
            edge[a].push_back(b);
        }
        ans = 0;
        dfs(0, 0, k, n);
        return ans;
        
        
    }
};
```