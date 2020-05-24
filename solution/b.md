# Problem
[Link](https://leetcode-cn.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/)

# Solution
* 直接模拟
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    bool parse(char ch) {
        if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
            return 1;
        }
        return 0;
    }
    
    int maxVowels(string s, int k) {
        int sum = 0;
        int ans = 0;
        for (int i = 0; i < k; ++i) {
            sum += parse(s[i]);
        }    
        ans = std::max(ans, sum);
        for (int i = k; i < s.size(); ++i) {
            sum += parse(s[i]);
            sum -= parse(s[i - k]);
            ans = std::max(ans, sum);
        }
        
        return ans;
    }
};
```