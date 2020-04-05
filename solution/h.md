# Problem
[Link](https://leetcode-cn.com/problems/stone-game-iii/)

# Solution

* 显然，需要求出n堆石子能拿到的最大值
* 不妨设dp[i]为从第i堆石子到最后一堆石子，能获取到的石子和的最大值，那么显然有dp[i] = max(dp[i], sum - dp[i + 1], sum - dp[i + 2], sum - dp[i + 3])
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    string stoneGameIII(vector<int>& stoneValue) {
        int n = stoneValue.size();
        std::vector<int> dp(n + 1, -0x3f3f3f3f);
        dp[n] = 0;
        int all_sum = 0;
        for (int i = n - 1; i >= 0; --i) {
            all_sum += stoneValue[i];
            for (int j = i; j < n && j < i + 3; ++j) {
                dp[i] = std::max(dp[i], all_sum - dp[j + 1]);
            }
        }
        if (dp[0] > all_sum - dp[0]) return "Alice";
        if (dp[0] == all_sum - dp[0]) return "Tie";
        return "Bob";
    }
};
```