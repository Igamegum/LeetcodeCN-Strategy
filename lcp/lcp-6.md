# Problem
[Link](https://leetcode-cn.com/problems/na-ying-bi/)

# Solution

* 直接除2就行
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int minCount(vector<int>& coins) {
        int ans = 0;
        for (int i = 0; i < coins.size(); ++i) {
            ans += coins[i] / 2;
            if (coins[i] & 1) ++ans;
        }
        return ans;
    }
};
```