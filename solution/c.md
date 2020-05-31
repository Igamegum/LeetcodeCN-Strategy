# Problem
[Link](https://leetcode-cn.com/problems/course-schedule-iv/)

# Solution
* 分别以N个点为起点DFS，将起点标记为搜过程中的点的先修课程，对于查询可以在O(1)的时间复杂度内完成
* 时间复杂度O(n*n)

# Code
```cpp
class Solution {
public:
    
    std::vector< std::vector<int> > edge;
    bool fa[110][110];
    bool vis[110];
    
    void dfs(int root, int cur) {
        fa[root][cur] = true;
        vis[cur] = true;
        for (int i = 0; i < edge[cur].size(); ++i) {
            if (!vis[edge[cur][i]]) {
                dfs(root, edge[cur][i]);    
            }
        }
    }
    
    vector<bool> checkIfPrerequisite(int n, vector<vector<int>>& prerequisites, vector<vector<int>>& queries) {
        edge = std::vector< std::vector<int> >(n, std::vector<int>(0));
        for (int i = 0; i < prerequisites.size(); ++i) {
            int a = prerequisites[i][0];
            int b = prerequisites[i][1];
            edge[a].push_back(b);
        }
        
       
        memset(fa, false, sizeof(fa));
        for (int i = 0; i < n; ++i) {
            memset(vis, false, sizeof(vis));
            dfs(i, i);
        }
        
        std::vector<bool> ans;
        for (int i = 0; i < queries.size(); ++i) {
            int a = queries[i][0];
            int b = queries[i][1];
            ans.push_back(fa[a][b]);
        }
        
        return ans;
    }
};
```