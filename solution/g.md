# Problem
[Link](https://leetcode-cn.com/problems/check-if-there-is-a-valid-path-in-a-grid/)

# Solution

* 并查集模拟，管道之间如果能相连，就并入同一个集合，判断点(0,0)跟点(n - 1, m - 1)是否在同一个集合即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:

    int dir[4][2] = {-1, 0, 1, 0, 0, -1, 0, 1};

    bool can_go(int dir, int nxt) {
        if (dir == 0) return nxt == 4 || nxt == 3 || nxt == 2;
        if (dir == 1) return nxt == 5 || nxt == 6 || nxt == 2;
        if (dir == 2) return nxt == 1 || nxt == 6 || nxt == 6;
        if (dir == 3) return nxt == 1 || nxt == 3 || nxt == 5;
        return false;
    }
    bool can_move(int dir, int nxt) {
        if (dir == 0) return nxt == 2 || nxt == 5 || nxt == 6;
        if (dir == 1) return nxt == 2 || nxt == 3 || nxt == 4;
        if (dir == 2) return nxt == 1 || nxt == 3 || nxt == 5;
        if (dir == 3) return nxt == 1 || nxt == 4 || nxt == 6;
        return false;
    }

    int bin[310 * 310];
    void init(int n, int m) {
        for (int i = 0; i <= n * m + 10; ++i) bin[i] = i;
    }
    int find(int x) {
        if (bin[x] == x ) return x;
        return bin[x] = find(bin[x]);
    }
    void merge(int x, int y) {
        int fx = find(x);
        int fy = find(y);
        bin[fx] = fy;
    }
    
    bool hasValidPath(vector<vector<int>>& grid) {
        int n = grid.size();    
        int m = grid[0].size();    
        init(n, m);

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                for (int k = 0; k < 4; ++k) {
                    int x = i + dir[k][0];
                    int y = j + dir[k][1];
                    if (x < 0 || x >= n || y < 0 || y >= m) continue;
                    if (can_move(k, grid[i][j]) && can_go(k, grid[x][y])) {
                        merge(x * m + y, i * m + j);
                    }
                }
            }
        }
        return find(0) == find(n * m  - 1);
    }
};
```