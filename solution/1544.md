# Problem
[Link](https://leetcode-cn.com/problems/make-the-string-great/)

# Solution
* 直接模拟，注意是不断操作，直到不能操作
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    bool is_lower(char ch) {
        return ch >= 'a' && ch <= 'z';
    }
    
    bool is_upper(char ch) {
        return ch >= 'A' && ch <= 'Z';
    }
    bool check(char lhs, char rhs) {
        if (is_lower(lhs) && is_upper(rhs)) {
            if (lhs - 'a' == rhs - 'A') return true;
        }
        if (is_upper(lhs) && is_lower(rhs)) {
            if (lhs - 'A' == rhs - 'a') return true;
        }
        return false;
    }
    std::string solve(const std::string& s) {
        std::string ans;
        int id = 0;
        while (id < s.size()) {
            if (id + 1 < s.size() && check(s[id], s[id + 1])) {
                id += 2;
            } else {
                ans += std::string(1, s[id]);
                ++id;
            }
        }
        return ans;
    }
    string makeGood(string s) {
        std::string ans = s;
        do {
            std::string pans = solve(ans);
            if (pans.size() == ans.size()) {
                ans = pans;
                break;
            }
            ans = pans;
        }while (true);
        return ans;
    }
};
```