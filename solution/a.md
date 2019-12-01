# Problem
[Link](https://leetcode-cn.com/problems/find-winner-on-a-tic-tac-toe-game/)

# Solution
* 直接模拟

# Code
```cpp
class Solution {
public:
    int dp[3][3];
    bool check(int num) {
        for (int i = 0; i < 3; ++i) {
            if (dp[i][0] == num && dp[i][1] == num && dp[i][2] == num) return true;
            if (dp[0][i] == num && dp[1][i] == num && dp[2][i] == num) return true;
        }
        if (dp[0][0] == num  && dp[1][1] == num && dp[2][2] == num) return true;
        if (dp[0][2] == num  && dp[1][1] == num && dp[2][0] == num) return true;
        return false;
    }
    string tictactoe(vector<vector<int>>& moves) {
        memset(dp, 0, sizeof(dp));
        for (int i = 0; i < moves.size(); ++i) {
            int x = moves[i][0];
            int y = moves[i][1];
            dp[x][y] = i & 1 ? 2 : 1;
        }
        if (check(1)) return "A";
        if (check(2)) return "B";
        if (moves.size() < 9) return "Pending";
        return "Draw";
        
    }
};
```