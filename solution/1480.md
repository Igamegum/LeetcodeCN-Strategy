# Problem
[Link](https://leetcode-cn.com/problems/running-sum-of-1d-array/)

# Solution
* 直接模拟
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        std::vector<int> ans;
        int sum = 0;
        for (int i = 0; i < nums.size(); ++i) {
            sum += nums[i];
            ans.push_back(sum);
        }
        return ans;
    }
};
```