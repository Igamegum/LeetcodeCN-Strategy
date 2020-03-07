# Problem
[Link](https://leetcode-cn.com/problems/how-many-numbers-are-smaller-than-the-current-number/)

# Solution

* 数据范围很小，直接模拟即可
* 时间复杂度O(n * n)

# Code
```cpp
class Solution {
public:
    vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
        std::vector<int> ans;
        for (int i = 0; i < nums.size(); ++i) {
            int cnt = 0;
            for (int j = 0; j < nums.size(); ++j) {
                if (nums[j] < nums[i]) ++cnt;
            }
            ans.push_back(cnt);
        }
        return ans;
    }
};
```