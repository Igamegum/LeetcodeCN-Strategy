# Problem
[Link](https://leetcode-cn.com/problems/number-of-substrings-with-only-1s/)

# Solution
* 直接分段计算出连续为1的子串的长度，然后求出贡献值
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    long long calc(long long x) {
        if (x == 1) return 1;
        long long ans = (1 + x) * x / 2;
        return ans;
    }
    int numSub(string s) {
        int cnt = 0;
        long long sum = 0;
        long long mod = 1e9 + 7;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '1') {
                ++cnt;
            } else {
                sum += calc(cnt);
                sum %= mod;
                cnt = 0;
            }
        }
        if (cnt) {
            sum += calc(cnt);
            sum %= mod;
        }
        return sum;
    }
};
```