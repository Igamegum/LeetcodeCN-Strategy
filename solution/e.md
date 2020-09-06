# Problem
[Link]()

# Solution
* 直接模拟
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    string modifyString(string s) {
        int n = s.size();
        char prev = 'a';
        for (int i =  0; i < s.size(); ++i) {
            if (s[i] == '?') {
                for (int j = 0; j < 26; ++j) {
                    char nt = 'a' + j;
                    if (nt != prev && ((i == s.size() - 1)||(i < s.size() - 1 && nt != s[i + 1]))) {
                        s[i] = nt;
                        break;
                    }
                }
            }
            prev = s[i];
        }
        return s;
    }
};
```