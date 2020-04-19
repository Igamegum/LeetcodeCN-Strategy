# Problem
[Link](https://leetcode-cn.com/problems/minimum-value-to-get-positive-step-by-step-sum/)

# Solution

* 首先假定需要的最小正整数是1，从左往右依次累加，如果当前累加和小于1，那么说明需要的正整数大小不足，补够差值即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int minStartValue(vector<int>& nums) {

        int ans = 1;
        int sum = 1;
        for (int i = 0; i < nums.size(); ++i) {
            sum += nums[i];
            if (sum < 1) {
                ans += (1 - sum);
                sum = 1;
            }
        }
        return ans;
    }
};
```