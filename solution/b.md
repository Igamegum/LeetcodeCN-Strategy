# Problem
[Link]()

# Solution
* 枚举区间的左端点和右端点，利用前缀和在O(1)的时间复杂度内求区间和
* 时间复杂度：O(n*n)

# Code
```cpp
class Solution {
public:
    int rangeSum(vector<int>& nums, int n, int left, int right) {
        
        for (int i = 1; i < n; ++i) {
            nums[i] += nums[i - 1];
        }
        
        std::vector<int> sq;
        //int n = nums.size();
        for (int i = 0; i < n; ++i) {
            for (int j = i; j < n; ++j) {
                int lhs = i == 0 ? 0 : nums[i - 1];
                sq.push_back(nums[j] - lhs);
            }
        }
        long long mod = 1e9 + 7;
        long long ans = 0;
        std::sort(sq.begin(), sq.end());
        for (int i = left - 1; i < right; ++i) {
            ans += sq[i];
            ans %= mod;
        }
        return ans;
    }
};

```