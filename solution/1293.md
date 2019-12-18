# Problem
[Link](https://leetcode-cn.com/problems/shortest-path-in-a-grid-with-obstacles-elimination)

# Solution

* 直接爆搜即可，注意hash需要带上剩余的k


# Code
```cpp
class Solution {
public:
    long long  hash_code(const int x, const int y, const int k) {
        long long ans = 0;
        ans = x * 1601 * 1601;
        ans += y * 1601;
        ans += k;
        return ans;
    }
    std::set<long long> used;
    struct Node
    {
        int x;
        int y;
        int k;
        int step;
    };
    
    int dir[4][2] = {-1, 0, 0, 1, 1, 0, -1, 0};
    
    int BFS(vector<vector<int>>& grid, int k) {
        std::queue<Node> q;
        Node node;
        node.x = 0;
        node.y = 0;
        node.k = (grid[0][0] == 0) ? k : k - 1;
        node.step = 0;
        q.push(node);
        
        int n = grid.size();
        int m = grid[0].size();
        
        while (!q.empty()) {
            node = q.front();
            q.pop();
            if (node.x == n - 1 && node.y == m - 1) return node.step;
            for (int i = 0; i < 4; ++i) {
                Node temp;
                temp.x    = node.x + dir[i][0];
                temp.y    = node.y + dir[i][1];
                temp.step = node.step + 1;
                temp.k    = node.k;
                if (temp.x < 0 || temp.x >= n || temp.y < 0 || temp.y >= m) continue;
                if (grid[temp.x][temp.y] == 1 && temp.k <= 0) continue;
                if (grid[temp.x][temp.y] == 1) --temp.k;
                long long  code = hash_code(temp.x, temp.y, temp.k);
                if (used.find(code) == used.end()) {
                    used.insert(code);
                    q.push(temp);
                }
            }
            
        }
        return -1;
    }
    int shortestPath(vector<vector<int>>& grid, int k) {
        return BFS(grid, k);
    }
};
```