# Problem
[Link](https://leetcode-cn.com/problems/minimum-time-visiting-all-points/)

# Solution

* 从点 i 到点 j，显然，能走对角线的情况下优先走对角线
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int minTimeToVisitAllPoints(vector<vector<int>>& points) {
        int ans = 0;
        for (int i = 1; i < points.size(); ++i) {
            int diff_x = std::abs(points[i][0] - points[i - 1][0]);
            int diff_y = std::abs(points[i][1] - points[i - 1][1]);
            int diff_min = std::min(diff_x, diff_y);
            int diff_max = std::max(diff_x, diff_y);
            ans += diff_min;
            ans += diff_max - diff_min;
        }
        return ans;
    }
};
```