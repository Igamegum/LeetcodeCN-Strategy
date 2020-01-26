
# Problem
[Link](https://leetcode-cn.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/)

# Solution

* 区间DP
* 考虑字符串s[i:j],假定s[i] = s[j],那么必定有dp[i][j] = dp[i + 1][j - 1];假定s[i] != s[j], 那么有 dp[i][j] = min(dp[i + 1][j], dp[i][j - 1]) + 1，相当于在s[i:j]的尾端补一个字符s[i],或者在头部补一个字符s[j],在两种方案间取较优
* 时间复杂度O(n*n)

# Code
```cpp
class Solution {
public:
    int minInsertions(string s) {
        
        int n = s.size();
        std::vector<std::vector<int>> dp(n, std::vector<int>(n, 0));
        for (int i = n - 1; i >= 0; --i) {
            dp[i][i] = 0;
            for (int j = i + 1; j < n; ++j) {
                if (s[i] == s[j]) {
                    dp[i][j] = dp[i + 1][j - 1];
                } else {
                    dp[i][j] = std::min(dp[i + 1][j], dp[i][j - 1]) + 1;
                }
            }
        }
        return dp[0][n - 1];
    }
};
```