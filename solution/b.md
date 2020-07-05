# Problem
[Link](https://leetcode-cn.com/problems/last-moment-before-all-ants-fall-out-of-a-plank/)

# Solution
* 蚂蚁相遇后掉头，相当于原来两只蚂蚁的身份交换后继续行走，所以可以看做两只蚂蚁直接穿过
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int getLastMoment(int n, vector<int>& left, vector<int>& right) {
        int ans = 0;
        for (int i = 0; i < left.size(); ++i) {
            ans = std::max(ans, left[i]);
        }
        for (int i = 0; i < right.size(); ++i) {
            ans = std::max(ans, n - right[i]);
        }
        return ans;
    }
};
```