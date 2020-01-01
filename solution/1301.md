# Problem
[Link](https://leetcode-cn.com/problems/deepest-leaves-sum/)

# Solution

* DP.本质上相当于从左上角出发，走到右下角，每次可以往右，往下，或者右下这三个方向走。
* 对于位置为 board[i][j]，其最大得分，相当于从 board[i - 1][j], board[i][j - 1], board[i - 1][j - 1]而来。注意，如果这三者中有多个最大值，则需要累加方法种数。
* 时间复杂度O(n * n)

# Code
```cpp
class Solution {
public:
    vector<int> pathsWithMaxScore(vector<string>& board) {
        int sum[110][110];
        int way[110][110];
        memset(sum, 0, sizeof(sum));
        memset(way, 0, sizeof(way));
        int n = board.size();
        board[0][0] = '0';
        board[n - 1][n - 1] = '0';
        
        sum[0][0] = 0;
        way[0][0] = 1;
        int mod = 1e9 + 7;
        
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                
                if (board[i][j] == 'X' || (i == 0 && j == 0)) continue;
                
                int sle = 0;
                int wle = 0;
                int sup = 0;
                int wup = 0;
                int slu = 0;
                int wlu = 0;
                
                if (i > 0 && board[i - 1][j] != 'X') {
                    sup = sum[i - 1][j];
                    wup = way[i - 1][j];
                } 
                
                if (j > 0 && board[i][j - 1] != 'X') {
                    sle = sum[i][j - 1];
                    wle = way[i][j - 1];
                }
                
                if (i > 0 && j > 0 && board[i - 1][j - 1] != 'X') {
                    slu = sum[i - 1][j - 1];
                    wlu = way[i - 1][j - 1];
                }
                
                int smax = std::max(sle, std::max(slu, sup));
                int wsum = 0;
                if (sle == smax) wsum += wle, wsum %= mod;
                if (slu == smax) wsum += wlu, wsum %= mod;
                if (sup == smax) wsum += wup, wsum %= mod;
                
                sum[i][j] = smax + board[i][j] - '0';
                way[i][j] = wsum;
            }
        }
        
        std::vector<int> ans;
        if (way[n - 1][n - 1]) {
            ans.push_back(sum[n - 1][n - 1]);
            ans.push_back(way[n - 1][n - 1]);    
        } else {
            ans.push_back(0);
            ans.push_back(0);
        }
        
        return ans;
    }
};
```