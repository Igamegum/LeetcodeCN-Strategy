# Problem
[Link](https://leetcode-cn.com/problems/maximum-number-of-occurrences-of-a-substring)

# Solution

* 首先，如果满足maxSize,那么一定满足minSize，而且答案是允许重叠的，所以maxSize可以直接忽略
* 直接枚举以i为起点，长度为minSize的串是否满足条件，利用map对子串进行hash并统计数量，最后求出最大的数值即可
* 时间复杂度O(n * logn * 26)

# Code
```cpp
class Solution {
public:

    bool check(const std::string str, const int mc) {
        std::set<char> S;
        for (int i = 0; i < str.size(); ++i) {
            S.insert(str[i]);
        }
        return S.size() <= mc;
    }
    
    int maxFreq(string s, int maxLetters, int minSize, int maxSize) {
        if (!s.size()) return 0;
        int ans = 0;
        std::map<std::string, int> mp;
        for (int i = 0; i < s.size(); ++i) {
                if (i + minSize - 1 >= s.size()) break;
                std::string str = s.substr(i, minSize);
                if (check(str, maxLetters)) {
                    mp[str]++;
                }
        }
        for (auto it = mp.begin(); it != mp.end(); ++it) {
            ans = std::max(ans, it->second);
        }
        return ans;

    }
};
```