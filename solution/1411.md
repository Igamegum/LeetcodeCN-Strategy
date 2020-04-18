# Problem
[Link](https://leetcode-cn.com/problems/number-of-ways-to-paint-n-x-3-grid/)

# Solution

* 直接暴力模拟每一层的颜色可解
* 直接统计规律也可解
* 首先，假定有颜色ABC三种，将同一层的涂色情况看做一个整体，那么同一层的涂色情况一定是ABC、ABA这两种形式，接下来只需要考虑下一层和上颜色不发生冲突即可
    * 假定上一层是ABC,下一层是ABC的形式，那么下一层只能是: BCA、CAB
    * 假定上一层是ABC,下一层是ABA的形式，那么下一层只能是: BCB、BAB
    * 假定上一层是ABA,下一层是ABC的形式，那么下一层只能是: BAC、CAB
    * 假定上一层是ABA,下一层是ABA的形式，那么下一层只能是: BAB、BCB、CAC
    * 那么不难得出规律 n_abc = 2 * abc + 2 * aba; n_aba = 2 * abc + 3 * aba
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int numOfWays(int n) {
        long long  abc = 6;
        long long  aba = 6;
        int mod = 1e9 + 7;
        for (int i = 2; i <= n; ++i) {
            long long t_abc = 2 * abc + 2 * aba; t_abc %= mod;
            long long t_aba = 2 * abc + 3 * aba; t_aba %= mod;
            abc = t_abc;
            aba = t_aba;
        }
        long long  ans = (abc + aba) % mod;
        return ans;
    }
};
```

```cpp
class Solution {
public:
    int numOfWays(int n) {
        int ans[n + 1][3][3][3];
        memset(ans, 0, sizeof(ans));
        for (int a = 0; a < 3; ++a)
            for (int b = 0; b < 3; ++b)
                for (int c = 0; c < 3; ++c)
                    if (a != b && c != b)
                        ans[1][a][b][c] = 1;
        
        int mod = 1e9 + 7;
        for (int i = 2; i <= n; ++i)
            for (int a = 0; a < 3; ++a)
                for (int b = 0; b < 3; ++b)
                    for (int c = 0; c < 3; ++c)
                        for (int aa = 0; aa < 3; ++aa)
                            for (int bb = 0;  bb< 3; ++bb)
                                for (int cc = 0;  cc < 3; ++cc)
                                    if (a != b && c != b) { //当前层颜色合法
                                        if (aa != bb && bb != cc) { //上一层颜色合法
                                            if (a != aa && b != bb && c != cc) {
                                                ans[i][a][b][c] += ans[i - 1][aa][bb][cc];
                                                ans[i][a][b][c] %= mod;
                                            }
                                        }
                                    }
        
        int res = 0;
        for (int a = 0; a < 3; ++a)
            for (int b = 0; b < 3; ++b)
                for (int c = 0; c < 3; ++c) {
                    res += ans[n][a][b][c];
                    res %= mod;
                }
                    
        return res;
    }
};
```