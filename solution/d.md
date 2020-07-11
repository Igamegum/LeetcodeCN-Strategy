# Problem
[Link]()

# Solution
* 
* 时间复杂度：O(n*sqrt(n))

# Code
```cpp
class Solution {
public:
    bool winnerSquareGame(int n) {
        std::vector<bool> dp(n + 1);
        dp[0] = false;
        for (int i = 1; i <= n; ++i) {
            bool can = false;
            for (int j = 1; j * j <= i; ++j) {
                if (dp[i - j * j] == false) {
                    can = true;
                    break;
                }
            }
            dp[i] = can;
        }
        return dp[n];
    }
};
```