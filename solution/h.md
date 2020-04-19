# Problem
[Link](https://leetcode-cn.com/problems/build-array-where-you-can-find-the-maximum-exactly-k-comparisons/)

# Solution

* 记忆化搜索即可
* 时间复杂度O(n * n * k)

# Code
```cpp
class Solution {
public:
    int mod = 1e9 + 7;
    int calc_pow(const int a, const int x) {
        if (x == 0) return 1;
        int val = a;
        for (int i = 1; i <= x; ++i) {
            val *= x;
            val %= mod;
        }
        return val;
    }
    
    int status[110][55][55];
    
    int dfs(int pre_max, int n, int k, const int m) {
        
        if (n == 0 && k == 0) return 1;
        if (n == 0 && k) return 0;
        if (k > n) return 0;
        
        if (pre_max >= 1) {
            if (m - pre_max < k) return 0;
            if (status[pre_max][n][k] != -1) return status[pre_max][n][k];
        }
                
        int total = 0;

        //在这个位置消耗一次
        if (pre_max < m && k) {
            for (int i = std::max(pre_max + 1, 1); i <= m; ++i) {
                total += dfs(i, n - 1, k - 1, m);
                total %= mod;
            }
        }
        
        //不消耗
        if (pre_max >= 1) {
            for (int i = 1; i <= pre_max; ++i) {
                total += dfs(pre_max, n - 1, k, m);    
                total %= mod;
            }
        }
        
        if (pre_max != -1){
            status[pre_max][n][k] = total % mod;
        }
        
        return total % mod;
            
    }
    
    int numOfArrays(int n, int m, int k) {
        if (k == 0) return 0;
        memset(status, -1, sizeof(status));
        return dfs(-1, n, k, m);
    }   
};
```