# Problem
[Link](https://leetcode-cn.com/problems/number-of-good-pairs/)

# Solution
* 直接模拟
* 时间复杂度：O(n*n)

# Code
```cpp
class Solution {
public:
    int numIdenticalPairs(vector<int>& nums) {
        int ans = 0;
        for (int i = 0; i < nums.size(); ++i) {
            for (int j = i + 1; j < nums.size(); ++j) {
                if (nums[i] == nums[j]) {
                    ++ans;
                }
            }
        }
        return ans;
    }
};
```