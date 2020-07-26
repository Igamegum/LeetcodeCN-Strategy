# Problem
[Link]()

# Solution
* 直接模拟
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    string restoreString(string s, vector<int>& indices) {
        int n = s.size();
        std::vector<char> ch(n);
        for (int i = 0; i < s.size(); ++i) {
            ch[indices[i]] = s[i];
        }
        std::string ans;
        for (int i = 0; i < ch.size(); ++i) {
            ans += std::string(1, ch[i]);
        }
        return ans;
    }
};

```