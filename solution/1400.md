# Problem
[Link](https://leetcode-cn.com/problems/construct-k-palindrome-strings/)

# Solution

* 直接统计每个字符出现的次数，出现奇数次的字符的数量不能超过K
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    bool canConstruct(string s, int k) {
        if (s.size() < k) return false;
        std::map<char, int> mp;
        for (int i = 0; i < s.size(); ++i) {
            ++mp[s[i]];
        }
        int odd = 0;
        for (auto it = mp.begin(); it != mp.end(); ++it) {
            if (it->second & 1) ++odd;
        }
        return odd <= k;
    }
};
```