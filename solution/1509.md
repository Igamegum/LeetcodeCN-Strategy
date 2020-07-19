# Problem
[Link](https://leetcode-cn.com/problems/minimum-difference-between-largest-and-smallest-value-in-three-moves/)

# Solution
* 首先必定是将左右两端的数字尽量修改成跟中间的数字一样的值，直接枚举左右两端分别修改的数字的数量
* 时间复杂度：Omax(nlogn，K)，K为操作次数

# Code
```cpp
class Solution {
public:
    int minDifference(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        if (nums.size() <= 4)  return 0;
        int n = nums.size();
        
        int ans = nums[n - 1] - nums[0];
        for (int L = 0; L <= 3; ++L) {
            int lhs = nums[L];
            int rhs = nums[n - 1 - (3 - L)];
            ans = std::min(ans, rhs - lhs);
        }
        return ans;
        
    }
};

```