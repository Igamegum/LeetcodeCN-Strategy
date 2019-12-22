# Problem
[Link](https://leetcode-cn.com/problems/find-numbers-with-even-number-of-digits/)

# Solution

* 直接模拟即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int len(const int val) {
        std::stringstream ss;
        ss << val;
        return ss.str().size();
    }
    int findNumbers(vector<int>& nums) {
        int ans = 0;
        for (int i = 0; i < nums.size(); ++i) {
            int val = len(nums[i]);
            if ((val % 2) == 0 ) {
                ++ans;
            }
        }
        return ans;
    }
};
```