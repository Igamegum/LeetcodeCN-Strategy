# Problem
[Link](https://leetcode-cn.com/problems/check-if-a-word-occurs-as-a-prefix-of-any-word-in-a-sentence/)

# Solution
* 直接模拟
* 时间复杂度O(n^n)

# Code
```cpp
class Solution {
public:
    int isPrefixOfWord(string sentence, string searchWord) {
        std::vector<std::string> strs;
        std::stringstream ss;
        for (int i = 0; i < sentence.size(); ++i) {
            if (sentence[i] == ' ') {
                if (ss.str().size()) strs.push_back(ss.str());
                ss.str("");
            } else {
                ss << sentence[i];
            }
        }
        
        if (ss.str().size()) strs.push_back(ss.str());
        
        for (int i = 0; i < strs.size(); ++i) {
            if (strs[i].find(searchWord) == 0) {
                return i + 1;
            }
        }
        
        return -1;
    }
};
```