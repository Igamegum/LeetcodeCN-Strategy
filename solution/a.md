
# Problem
[Link](https://leetcode-cn.com/problems/decrypt-string-from-alphabet-to-integer-mapping/)

# Solution

* 从后往前直接模拟即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    string freqAlphabets(string s) {
        std::string ans;
        for (int i = s.size() - 1; i >= 0; ) {
            if (s[i] == '#') {
                
                int val = (s[i - 2] - '0') * 10 + (s[i - 1] - '0');
                ans += (val - 10) + 'j';
                i -= 3;
            } else {

                int val = (s[i] - '0');
                ans += (val - 1) + 'a';
                i--;
            }
        }
        std::reverse(ans.begin(), ans.end());
        return ans;
    }
};
```