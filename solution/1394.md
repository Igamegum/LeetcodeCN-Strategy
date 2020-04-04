# Problem
[Link](https://leetcode-cn.com/problems/find-lucky-integer-in-an-array/)

# Solution

* 直接map模拟即可
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    int findLucky(vector<int>& arr) {
        std::map<int, int> mp;
        for (int i = 0; i < arr.size(); ++i) {
            ++mp[arr[i]];
        }
        int ans = -1;
        for (auto it = mp.begin(); it != mp.end(); ++it) {
            if (it->first == it->second) {
                ans = std::max(ans, it->second);
            }
        }
        return ans;
    }
};
```