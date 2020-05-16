# Problem
[Link]()

# Solution
* 直接枚举，两两gcd为1即可
* 时间复杂度O(n * n)

# Code
```cpp
class Solution {
public:
    int gcd(int x, int y) {
        if (!y) return x;
        return gcd(y, x % y);
    }
    vector<string> simplifiedFractions(int n) {
        std::vector<string> ans;
        for (int i = 1; i <= n; ++i) {
            for (int j = i + 1; j <= n; ++j) {
                if (gcd(i, j) == 1) {
                    std::stringstream ss;
                    ss << i << "/" << j;
                    ans.push_back(ss.str());
                }
            }
        }
        return ans;
    }
};
```