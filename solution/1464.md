# Problem
[Link](https://leetcode-cn.com/problems/maximum-product-of-two-elements-in-an-array/)

# Solution
* 排序后直接取最大的两个数即可
* 时间复杂度O(n*logn)

# Code
```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int n = nums.size();
        std::sort(nums.begin(), nums.end());
        return (nums[n - 1] - 1) * (nums[n - 2] - 1);
    }
};
```