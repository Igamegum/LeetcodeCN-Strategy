# Problem
[Link](https://leetcode-cn.com/problems/constrained-subsequence-sum/)

# Solution

* 滑动窗口
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    int longestSubarray(vector<int>& nums, int limit) {
        std::multiset<int> S;
        S.insert(nums[0]);
        int ans = 1;
        int L = 0;

        for (int i = 1; i < nums.size(); ++i) {
            S.insert(nums[i]);
            while (L < i && *S.rbegin() - *S.begin() > limit) {
                S.erase(S.find(nums[L]));
                ++L;
            }
            if (*S.rbegin() - *S.begin() <= limit) {
                ans = std::max(ans, i - L + 1);
            }
        }
        
        return ans;
    }
};
```