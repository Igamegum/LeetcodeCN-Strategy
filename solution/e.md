# Problem
[Link](https://leetcode-cn.com/problems/minimum-subsequence-in-non-increasing-order/)

# Solution

* 显然，先排序，然后从后往前取即可
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    vector<int> minSubsequence(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int sum = 0;
        for (int i = 0; i < nums.size(); ++i) sum += nums[i];
            
        std::vector<int> ans;
        int cur = 0;
        for (int i = nums.size() - 1; i >= 0; --i) {
            ans.push_back(nums[i]);
            cur += nums[i];
            if (cur  > sum - cur) break;
        }
        return ans;
    }
};
```