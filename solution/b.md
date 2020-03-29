# Problem
[Link](https://leetcode-cn.com/problems/count-number-of-teams/)

# Solution

* 数据范围很小，直接模拟
* 时间复杂度O(n^3)

# Code
```cpp
class Solution {
public:
    int numTeams(vector<int>& rating) {
        int ans = 0;
        for (int i = 0; i < rating.size(); ++i) {
            for (int j = i + 1; j < rating.size(); ++j) {
                for (int k = j + 1; k < rating.size(); ++k) {
                    if (rating[i] < rating[j] && rating[j] < rating[k]) {
                        ++ans;
                    }
                    if (rating[i] > rating[j] && rating[j] > rating[k]) {
                        ++ans;
                    }
                    
                }
            }
        }
        return ans;
    }
};
```