# Problem
[Link](https://leetcode-cn.com/problems/check-if-all-1s-are-at-least-length-k-places-away/)

# Solution

* 直接模拟即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    bool kLengthApart(vector<int>& nums, int k) {
        int n = nums.size(); 
        int index = -n  - 100;
        for (int i = 0; i < nums.size(); ++i) {
            if (nums[i] == 1 && i - index - 1 < k) return false;
            if (nums[i] == 1) {
                index = i;
            }
        }
        
        return true;
    }
};
```