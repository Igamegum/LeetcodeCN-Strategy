# Problem
[Link]()

# Solution
* 利用前缀和和后缀和的思想，分别维护以i为结尾的前缀和后缀中不同的字符的数量，接着枚举切割点即可
* 时间复杂度：O(nlog26)

# Code
```cpp
class Solution {
public:
    int numSplits(string s) {
        
        int n = s.size();
        if (n == 1) return 0;
        std::vector< int > prev(n, 0);
        std::vector< int > suff(n, 0);
        std::set<char> S;
        S.clear();
        for (int i = 0; i < s.size(); ++i) {
            S.insert(s[i]);
            prev[i] = S.size();
        } 
        S.clear();
        for (int i = n - 1; i >= 0; --i) {
            S.insert(s[i]);
            suff[i] = S.size();
        }
        int ans = 0;
        for (int i = 0; i < n - 1; ++i) {
            int lhs = prev[i];
            int rhs = suff[i + 1];
            if (lhs == rhs) ++ans;
        }
        return ans;
        
    }
};
```