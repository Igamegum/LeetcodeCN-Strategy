# Problem
[Link]()

# Solution
* 不妨设dp[c][i][j]代表在第c层的时候，机器人1在位置i,机器人2在位置j，那么显然，对于grid[c][i]的位置，可以由grid[c - 1][i - 1], grid[c - 1][i], grid[c - 1][i + 1]而来，grid[c][j]的位置同理
* 枚举机器人的位置，直接暴力DP即可
* 时间复杂度O(n*n*m*9)

# Code
```cpp
class Solution {
public:
    int dp[71][71][71];
    int cherryPickup(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        memset(dp, -1, sizeof(dp));
        
        int ans = 0;
        dp[0][0][m - 1] = grid[0][0] + grid[0][m - 1];
        for (int floor = 1; floor < n; ++floor) {
            for (int i = 0; i < m; ++i) {
                for (int j = 0; j < m; ++j) {
                    for (int p = -1; p <= 1; ++p) {
                        for (int q = -1; q <= 1; ++q) {
                            int a = i + p;
                            int b = j + q;
                            if (a < 0 || a >= m || b < 0 || b >= m) continue;
                            if (dp[floor - 1][a][b] == -1) continue;
                            int val = dp[floor - 1][a][b] + grid[floor][i] + grid[floor][j];
                            if (i == j) val -= grid[floor][j];
                            dp[floor][i][j] = std::max(dp[floor][i][j], val);
                            ans = std::max(ans, dp[floor][i][j]);
                        }
                    }
                }
            }
        }
        
        return ans;
        
    }
};
```