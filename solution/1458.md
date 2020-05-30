# Problem
[Link](https://leetcode-cn.com/problems/max-dot-product-of-two-subsequences/)

# Solution
* DP
* 不妨设dp[i][j]代表一定取nums1[i - 1]和nums2[j - 1]的最优结果，max_val[i][j]代表值考虑nums1前i个数和nums2前j个数的最优结果，那么一定有dp[i][j] = max(0, max_val[i - 1][j - 1]) + nums1[i - 1] * nums2[j - 1];
* max_val[i][j] = max(max_val[i - 1][j - 1], max_val[i - 1][j], max_val[i][j - 1], dp[i][j])
* 时间复杂度O(n*m)

# Code
```cpp
class Solution {
public:
    int maxDotProduct(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        int m = nums2.size();
        
        std::vector< std::vector<int> > dp(n + 1, std::vector<int>(m + 1, 0));
        std::vector< std::vector<int> > max_val(n + 1, std::vector<int>(m + 1, -0x3f3f3f3f));
        
        int ans = -0x3f3f3f3f;
        
        for (int i = 1; i <= n; ++i) {
            for (int j = 1; j <= m; ++j) {
                if (i == 1 || j == 1) {
                    dp[i][j] = nums1[i - 1] * nums2[j - 1];
                } else {
                    dp[i][j] = std::max(max_val[i - 1][j - 1], 0) + nums1[i - 1] * nums2[j - 1];
                }
                
                max_val[i][j] = std::max(max_val[i][j], dp[i][j]);
                max_val[i][j] = std::max(max_val[i][j], max_val[i][j - 1]);
                max_val[i][j] = std::max(max_val[i][j], max_val[i - 1][j]);
                
                ans = std::max(ans, max_val[i][j]);
            }
        }
        
        return ans;
        
    }
};
```