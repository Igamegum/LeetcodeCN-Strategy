# Problem
[Link](https://leetcode-cn.com/problems/increasing-decreasing-string/)

# Solution

* 统计每个字符的出现次数，然后从小到大取一遍，再从大到小取一遍即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    string sortString(string s) {
        std::vector<int> num(26, 0);
        for (int i = 0; i < s.size(); ++i) {
            ++num[s[i] - 'a'];
        }

        std::string ans;
        int total = s.size();
        while (total > 0) {
            
                for (int i = 0; i < 26; ++i) {
                    if (num[i]) {
                        ans += ('a' + i);
                        --num[i];
                        --total;
                    }
                }    
            
                for (int i = 26 - 1; i >= 0; --i) {
                    if (num[i]) {
                        ans += ('a' + i);
                        --num[i];
                        --total;
                    }
                }    
            
        }
        return ans;
    }
};
```