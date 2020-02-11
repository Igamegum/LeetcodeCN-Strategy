# Problem
[Link](https://leetcode-cn.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/)

# Solution

* 直接累加两个字符串相同字母的数量差的和，答案就是这个和除2
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int minSteps(string s, string t) {
        int ss[26];
        memset(ss, 0, sizeof(ss));
        for (int i = 0; i < s.size(); ++i) ++ss[s[i] - 'a'];
        
        int tt[26];
        memset(tt, 0, sizeof(tt));
        for (int i = 0; i < t.size(); ++i) ++tt[t[i] - 'a'];
        
        int ans = 0;
        for (int i = 0; i < 26; ++i) {
            ans += std::abs(ss[i] - tt[i]);
        }
        
        return ans / 2;
    }
};
```