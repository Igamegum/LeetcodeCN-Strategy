# Problem
[Link](https://leetcode-cn.com/problems/minimum-number-of-days-to-make-m-bouquets/)

# Solution
* 直接二分答案
* 时间复杂度O(nlogbloomDay[i])

# Code
```cpp
class Solution {
public:
    int minDays(vector<int>& bloomDay, long long  m, long long  k) {
        int n = bloomDay.size();
        long long total = m * k;
        if (total > n) return -1;
        
        int max_val = bloomDay[0];
        for (int i = 0; i < bloomDay.size(); ++i) {
            max_val = std::max(max_val, bloomDay[i]);
        }
        
        int L = 1;
        int R = max_val;
        int ans = max_val;
        std::vector<bool> can(n, false);
        while (L <= R) {
            
            int mid = (L + R) >> 1;
            
            for (int i = 0; i < bloomDay.size(); ++i) {
                can[i] = bloomDay[i] <= mid;
            }
            
            int sum = 0;
            int cnt = 0;
            for (int i = 0; i < bloomDay.size(); ++i) {
                if (can[i]) {
                    ++sum;
                    if (sum >= k) {
                        ++cnt;
                        sum = 0;
                    }
                } else {
                    sum = 0;
                }
                
            }
            if (cnt >= m) {
                ans = std::min(ans, mid);
                R = mid - 1;
            } else {
                L = mid + 1;
            }
        }
        return ans;
    }
};
```