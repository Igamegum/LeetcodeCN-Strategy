# Problem
[Link](https://leetcode-cn.com/problems/number-of-ways-to-split-a-string/)

# Solution
* 首先直接将字符串分割为3个数字1相等的部分（这里需要排除多余的0）
* 那么可有得到4个端点：第一个段的尾端点，第二个段的头端点，第二个段的尾端点，第三个段的头端点
* 那么答案其实很简单了，就是第一个端点和第二个端点之间的0的划分方案数 乘以 第三个端点和第四个端点之间的0的划分方案数
* 时间复杂度：O(n)

# Code
```cpp
static int mod = 1e9 + 7;
class Solution {
public:
    
    int calc(const long long  num) {
        long long x = num * (num - 1);
        long long ans = x / 2;
        return ans % mod;
    }
    int numWays(string s) {
        int n = s.size();
        if (s.size() < 3) return 0;
        int cnt = 0;
        for (int i = 0; i < n; ++i) {
            if (s[i] == '1') ++cnt;
        }
        if ((cnt % 3) != 0) return 0;
        
        if (cnt == 0) {
            return calc(n - 2 + 1);
        }
        
        const int base = cnt / 3;
        std::vector<int> pos;
        int one = 0;
        for (int i = 0; i < n; ++i) {
            if (s[i] == '1') {
               if (one == 0 && pos.size()) {
                    pos.push_back(i);
                }
                ++one;
            }
            if (one == base) {
                if (pos.size() <= 3) pos.push_back(i);
                one = 0;
            }
        }
        /*for (int i = 0; i < pos.size(); ++i) {
            std::cout << pos[i] << std::endl;
        }*/
        long long a = pos[1] - pos[0];
        long long b = pos[3] - pos[2];
        long long ans = (a * b) % mod;
        
        return ans;
        
    }
};
```