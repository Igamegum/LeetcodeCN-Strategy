# Problem
[Link](https://leetcode-cn.com/problems/minimum-difficulty-of-a-job-schedule/)

# Solution

* DP
* 不防设dp[i][j]代表从0到第i项任务，刚好排期j天的最优解。那么状态转移只需要考虑以下两种情况。
* 假定前i-1项任务排了j-1天，第i项任务排在第j天，那么显然有dp[i][j] = dp[i - 1][j - 1] + jobDifficulty[i]
* 假定前i-1项任务排了j天，  第i项任务排在第j天，那么需要枚举一个最优值。 dp[i][j] = dp[x][j - 1] + max(jobDifficulty[y]){ 0 <= x <= i - 1, x < y <= i}
* 时间复杂度O(n * d)

# Code
```cpp
class Solution {
public:
    
    int dp[330][11];
    
    int minDifficulty(vector<int>& jobDifficulty, int d) {
        
        if (jobDifficulty.size() <= 0) return -1;
        
        memset(dp, -1, sizeof(dp));
        dp[1][1] = jobDifficulty[0];
        
        for (int i = 1; i < jobDifficulty.size(); ++i) {
            int id = i + 1;
            for (int j = 1; j <= d; ++j) {

                int a = 0x3f3f3f3f;
                int c = 0x3f3f3f3f;
                dp[id][j] = 0x3f3f3f3f;
                
                if (dp[id - 1][j] != -1) {
                    if (j == 1) {
                        a = std::max(dp[id - 1][j], jobDifficulty[i]);
                    }
                    else {
                        int min_val = 0x3f3f3f3f;
                        int max_job = jobDifficulty[i];
                        for (int k = id - 1; k >= 1; --k) {
                            if (dp[k][j - 1] != -1) {
                                max_job = std::max(max_job, jobDifficulty[k]);
                                min_val = std::min(min_val, dp[k][j - 1] + max_job);
                            }
                        }
                        a = min_val;
                    }
                }
                
                if (dp[id - 1][j - 1] != -1) {
                    c = dp[id - 1][j - 1] + jobDifficulty[i];
                } 
                
                dp[id][j] = std::min(dp[id][j], a);
                dp[id][j] = std::min(dp[id][j], c);
                
                if (dp[id][j] == 0x3f3f3f3f) dp[id][j] = -1;
            }
        }
        
        return dp[jobDifficulty.size()][d];
    }
};
```