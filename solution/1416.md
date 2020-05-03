# Problem
[Link](https://leetcode-cn.com/problems/restore-the-array/)

# Solution

* 简单DP，不妨设dp[i]代表s[0:i]合法的方案数，那么只需要不断枚举切割点即可，显然有dp[i] +=  dp[0:i - 1]
* 时间复杂度O(n^2)

# Code
```cpp
class Solution {
public:
    int numberOfArrays(string s, int k) {
        int mod = 1e9 + 7;
        int n = s.size();
        std::vector<long long> dp(n + 1, 0);
        for (int i = 1; i <= n; ++i) {
            long long base = 1;
            long long sum = 0;
            for (int j = i; j >= 1; --j) {
                if (base > k) break;
                long long pre = s[j - 1] - '0';
                sum += (pre) * base;
                base *= 10;
                if (sum >= 1 && sum <= k && pre != 0) {
                    dp[i] += dp[j - 1];
                    if (j == 1) ++dp[i];
                    dp[i] %= mod;
                }
                if (sum > k) break;
            }
        }
        return dp[n];
    }
};
```