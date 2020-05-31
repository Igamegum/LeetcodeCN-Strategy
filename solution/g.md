# Problem
[Link](https://leetcode-cn.com/problems/reorder-routes-to-make-all-paths-lead-to-the-city-zero/)

# Solution
* 这里比较有趣，不妨考虑从0点出发，能直接到达的点都是需要变更方向的路线。如果点0不能到达点a，并且点a能到达点b，那么边[0, a]是需要变更方向的，边[a, b]不需要变更方向，此时记点a不能直接从0到达，点b能直接从0到达
* 由于只有n - 1 条边，直接从点0开始BFS，判断点0能直接到达的点的数量即可
* 时间复杂度O(n*n)

# Code
```cpp
class Solution {
public:
    std::vector< std::vector<int> > edge;
    std::vector< std::vector<int> > fedge;
    
    std::vector<bool> can;
    std::vector<bool> vis;
    
    void bfs() {
        std::queue<int> q;
        q.push(0);
        vis[0] = true;
        while (!q.empty()) {
            int nw = q.front();
            q.pop();
            for (int i = 0; i < edge[nw].size(); ++i) {
                int nt = edge[nw][i];
                if (!vis[nt]) {
                    can[nt] = true;
                    vis[nt] = true;
                    q.push(nt);
                }
            }
            
            for (int i = 0; i < fedge[nw].size(); ++i) {
                int nt = fedge[nw][i];
                if (!vis[nt]) {
                    vis[nt] = true;
                    q.push(nt);
                }
            }
        }
    }
    
    int minReorder(int n, vector<vector<int>>& connections) {
        edge = std::vector< std::vector<int> > (n, std::vector<int>(0));
        fedge = std::vector< std::vector<int> > (n, std::vector<int>(0));
        
        can = std::vector<bool>(n, false);
        vis = std::vector<bool>(n, false);
        
        for (int i = 0; i < connections.size(); ++i) {
            int s = connections[i][0];
            int t = connections[i][1];
            edge[s].push_back(t);
            fedge[t].push_back(s);
        }
        
        bfs();
        int cnt = 0;
        for (int i = 0; i < n; ++i) {
            cnt += can[i] ? 1 : 0;
        }
        
        return cnt;
        
    }
};

```