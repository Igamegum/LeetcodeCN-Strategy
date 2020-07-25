# Problem
[Link]()

# Solution
* 简单DP
* 首先直接将数组中的每个数字对2取模，变成0 1 数组
* 不妨设odd[i] 代表以i为结尾的子数组和为奇数的数量，zro[i]代表以i为结尾的子数组和为偶数的数量
* 当arr[i]为1的时候，odd[i] = zro[i - 1] + 1;zro[i] = odd[i - 1];
* 当arr[i]为0的时候，odd[i] = zro[i - 1];zro[i] = odd[i - 1] + 1;
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    int numOfSubarrays(vector<int>& arr) {
        int n = arr.size();
        for (int i = 0; i < arr.size(); ++i) {
            arr[i] = arr[i] % 2;
        }
        std::vector<int> odd(n + 1, 0);
        std::vector<int> zro(n + 1, 0);
        int mod = 1e9 + 7;
        for (int i = 1; i <= n; ++i) {
            if (arr[i - 1] & 1) {
                odd[i] = zro[i - 1] + 1;
                zro[i] = odd[i - 1];
            } else {
                odd[i] = odd[i - 1];
                zro[i] = zro[i - 1] + 1;
            }
            odd[i] %= mod;
            zro[i] %= mod;
        }
        int ans = 0;
        for (int i = 1; i <= n; ++i) {
            ans += odd[i];
            ans %= mod;
        }
        return ans;

    }
};
```