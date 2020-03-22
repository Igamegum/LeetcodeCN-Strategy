# Problem
[Link](https://leetcode-cn.com/problems/create-target-array-in-the-given-order/)

# Solution

* 模拟list的操作，由于数据范围很小，直接用vector暴力即可
* 时间复杂度O(n * n)

# Code
```cpp
class Solution {
public:
    vector<int> createTargetArray(vector<int>& nums, vector<int>& index) {
        std::vector<int> ans;
        for (int i = 0; i < index.size(); ++i) {
            std::vector<int> tmp;
            for (int j = 0; j < index[i]; ++j) tmp.push_back(ans[j]);
            tmp.push_back(nums[i]);
            for (int j = index[i]; j < ans.size(); ++j) tmp.push_back(ans[j]);
            ans = tmp;
        }
        return ans;
    }
};
```