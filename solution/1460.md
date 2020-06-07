# Problem
[Link](https://leetcode-cn.com/problems/make-two-arrays-equal-by-reversing-sub-arrays/)

# Solution
* 显然，每个数字都能变换到任意位置，所以只需要比较每种数字出现的次数是否一样即可
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    bool canBeEqual(vector<int>& target, vector<int>& arr) {
        std::map<int, int> mp1;
        std::map<int, int> mp2;
        for (int i = 0; i < target.size(); ++i) {
            ++mp1[target[i]];
            ++mp2[arr[i]];
        }
        
        if (mp1.size() != mp2.size()) return false;
        for (auto it = mp1.begin(); it != mp1.end(); ++it) {
            int val = it->first;
            int num = it->second;
            if (mp2.find(val) == mp2.end()) return false;
            if (mp2[val] != num) return false;
        }
        
        return true;
    }
};
```