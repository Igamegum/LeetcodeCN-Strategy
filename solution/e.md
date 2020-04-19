# Problem
[Link](https://leetcode-cn.com/problems/reformat-the-string/)

# Solution

* 将字符按照字母和数字分类，然后直接模拟即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    string reformat(string s) {
        std::vector<char> ch;
        std::vector<char> num;
        
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] >= 'a' && s[i] <= 'z') {
                ch.push_back(s[i]);
            } else {
                num.push_back(s[i]);
            }
        }
        int diff = ch.size() - num.size();
        if (abs(diff) > 1) return "";
        
        std::string ans;
        if (ch.size() > num.size()) {
            for (int i = 0; i < num.size(); ++i) {
                ans += ch[i];
                ans += num[i];
            }
            if (ch.size() != num.size()) ans += ch[ch.size() - 1];
        } else {
            for (int i = 0; i < ch.size(); ++i) {
                ans += num[i];
                ans += ch[i];
            }
            if (ch.size() != num.size()) ans += num[num.size() - 1];
        }
        return ans;
    }
};
```