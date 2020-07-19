# Problem
[Link](https://leetcode-cn.com/problems/stone-game-iv/)

# Solution
* 不妨设dp[i]代表剩余石子数为i的时候，是否先手必胜
* 首先，必定有dp[0] = false，剩余石子数为0的时候，先手无法操作，必败
* 对于dp[i],枚举每次能操作的数量X（X 为完全平方数， X <= i），如果dp[i - X] = false，代表先手在i个石子的情况下拿走X个石子后，后手会面临必败的局面，那么对于i个石子的情况下，先手必胜
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