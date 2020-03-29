# Problem
[Link](https://leetcode-cn.com/problems/find-the-distance-value-between-two-arrays/)

# Solution

* 直接模拟即可。
* 或者维护每个数字出现的次数，然后利用前缀和的思想，快速求出某个范围内的数字是否出现过
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int findTheDistanceValue(vector<int>& arr1, vector<int>& arr2, int d) {
        std::vector<int> sum(1e6 + 200, 0);
        int base = 1e3 + 100 + 1;
        for (int i = 0; i < arr2.size(); ++i) {
            arr2[i] += base;
            sum[arr2[i]] += 1;
        }
        
        for (int i = 1; i < 1e6 + 200; ++i) {
            sum[i] += sum[i - 1];
        }
        
        int ans = 0;
        for (int i = 0; i < arr1.size(); ++i) {
            int st = arr1[i] + base - d;
            int ed = arr1[i] + base + d;
            int prefix = sum[ed] - sum[st - 1];
            if (prefix <= 0) ++ans;
        } 
        return ans;
    }
};
```