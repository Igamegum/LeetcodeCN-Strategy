# Problem
[Link](https://leetcode-cn.com/problems/reducing-dishes/)

# Solution

* 显然，先排序，然后从后往前枚举起点
* 如果维护一个后缀和，枚举的时间复杂度可以降到O(n), 这里数据范围很小，直接暴力枚举即可
* 时间复杂度O(nlogn) or O(n^2)

# Code
```cpp
class Solution {
public:
    int maxSatisfaction(vector<int>& satisfaction) {
        std::sort(satisfaction.begin(), satisfaction.end());
        int ans = 0;
        for (int i = 0; i < satisfaction.size(); ++i) {
            int sum = 0;
            for (int j = i; j < satisfaction.size(); ++j) {
                sum += satisfaction[j] * (j - i + 1);
            }
            ans = std::max(ans, sum);
        }
        return ans;
    }
};
```