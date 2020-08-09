# Problem
[Link](https://leetcode-cn.com/problems/can-convert-string-in-k-moves/)

# Solution
* 记录转换到没一个字符串需要的操作数,假定操作数是x，然后x有y次，判断K是否满足可以有y个模26为x数即可
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    bool canConvertString(string s, string t, int k) {
        if (s.size() != t.size()) return false;
        std::vector<int> arr;
        for (int i = 0; i < s.size(); ++i) {
            int num = (t[i] + 26 - s[i]) % 26;
            arr.push_back(num);
        }
        std:map<int, int > mp;
        for (int i = 0; i < arr.size(); ++i) {
            if (arr[i] == 0) {
                continue;
            }
            ++mp[arr[i]];
            
        }
        
        for (auto item : mp) {
            int numm = item.first;
            int twice = item.second;
            if (twice - k / 26 >= 2) return false;
            if (k / 26 < twice) {
                if (k % 26 < numm) {
                    return false;
                }
            }
        }
        return true;
    }
};
```