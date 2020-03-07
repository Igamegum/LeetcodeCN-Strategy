# Problem
[Link](https://leetcode-cn.com/problems/find-the-longest-substring-containing-vowels-in-even-counts/)

# Solution

* 状态压缩
* 不妨设status为字符串 s 中的元音字母出现次数的奇偶性的压缩值，因为元音字母只有5个，所以status是一个只有5位的二进制数字
* 假定子串s[0:i] 和子串 s[0:j] 的状态值相同，那么子串 s[i+1:j]的status一定为0，相当于s[i+1:j]中的元音字母的出现次数一定为偶数
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:

    int dit_char(char a) {
        if (a == 'a') return 1 << 0;
        if (a == 'e') return 1 << 1;
        if (a == 'i') return 1 << 2;
        if (a == 'o') return 1 << 3;
        if (a == 'u') return 1 << 4;
        return 0;
    }
    
    int findTheLongestSubstring(string s) {
        std::vector<int> pos(1 << 5, -1);
        int status = 0;
        pos[status] = 0;
        int ans = 0;
        for (int i = 0; i < s.size(); ++i) {
            int base = dit_char(s[i]);
            status ^= base;
            if (pos[status] == -1) {
                pos[status] = i + 1;
            } else {
                ans = std::max(ans, i + 1 - pos[status]);
            }
        }
        
        return ans;
    }
};
```
