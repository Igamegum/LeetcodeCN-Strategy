# Problem
[Link](https://leetcode-cn.com/problems/check-if-a-string-contains-all-binary-codes-of-size-k/)

# Solution
* 枚举长度为K的子串，计算其从二进制转为10进制的数字，最后判断出现数字的种类数是否为2的K次方即可
* 时间复杂度O(n*k)

# Code
```cpp
class Solution {
public:
   int parse(const std::string& str) {
       int ans = 0;
       int K = str.size(); 
       int base = 1;
       for (int i = str.size() - 1; i >= 0; --i) {
           ans += (str[i] - '0') * base;
           base <<= 1;
       }
       return ans;
   }
    
    bool hasAllCodes(string s, int k) {
        if (s.size() < k) return false;
        std::set<int> S;
        for (int i = 0; i <= s.size() - k; ++i) {
            std::string sub = s.substr(i, k);
            S.insert(parse(sub));
        } 
        int base = 1 << k;
        return S.size() == base;
    }
    
};
```