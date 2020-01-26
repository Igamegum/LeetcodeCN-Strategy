# Problem
[Link](https://leetcode-cn.com/problems/remove-palindromic-subsequences/)

# Solution

* 因为可以删除子序列，而且字符串只由a或b组成，那么显然，最大的操作数不超过2(先删除所有的a，再删除所有的b)。
* 假定字符串本身就是回文串，那么操作数为 1;假定字符串本身就是空串，那么操作数为 0。
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    bool check(const std::string& s) {
        int p = 0;
        int q = s.size() - 1;
        while (p < q) {
            if (s[p] != s[q]) return false;
            ++p;
            --q;
        }
        
        return true;
    }
    int removePalindromeSub(string s) {
        if (s.size() <= 0) return 0;
        if (check(s)) return 1;
        return 2;
    }
};
```