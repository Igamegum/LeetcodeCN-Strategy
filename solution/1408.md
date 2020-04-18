# Problem
[Link](https://leetcode-cn.com/problems/string-matching-in-an-array/)

# Solution

* 直接模拟
* 时间复杂度O(n^2)

# Code
```cpp
class Solution {
public:
    vector<string> stringMatching(vector<string>& words) {
        std::vector<string> ans;
        
        for (int i = 0; i < words.size(); ++i) {
            for (int j = 0; j < words.size(); ++j) {
                if (i == j) continue;
                if (words[j].find(words[i]) != words[j].npos) {
                    ans.push_back(words[i]);
                    break;
                }
            }
        }
        
        return ans;
    }
};
```