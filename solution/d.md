# Problem
[Link](https://leetcode-cn.com/problems/palindrome-partitioning-iii/)

# Solution
* DP
* 不妨设dp[i][x]代表字符串s[0:i]分割了x次的最优值, cal[i][j]代表字符串[i:j]变成回文串需要修改的字符数量
* 枚举 j，将字符串分割为s[0:j]和s[j + 1:i],两部分，那么显然有dp[i][x] = min(dp[i][x], dp[j][x - 1] + cal[j + 1][i])


# Code
```cpp
class Solution {
public:
    int calc(const std::string &s) {
        int p = 0;
        int q = s.length() - 1;
        int ans = 0;
        while (p < q) {
            if (s[p] != s[q]) ++ans;
            p++;
            q--;
        }
        return ans;
    }
    

    int palindromePartition(string s, int k) {
        
        int cal[110][110];
        for (int i = 0; i < s.length(); ++i) {
            for (int j = i; j < s.length(); ++j) {
                cal[i][j] = calc(s.substr(i, j - i + 1));
            }
        } 

        std::vector< std::vector<int> > dp(s.length() + 1, std::vector<int>(k + 1, s.length()));
        dp[0][0] = 0;
        for (int i = 1; i <= s.length(); ++i) {
            for (int x = 1; x <= k; ++x) {
                for (int j = 0; j < i; ++j) {
                    dp[i][x] = std::min(dp[j][x - 1] + cal[j][i - 1], dp[i][x]);
                }
            }
        }
        
        return dp[s.length()][k];
    }
};
```