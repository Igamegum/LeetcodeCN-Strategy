# Problem
[Link](https://leetcode-cn.com/problems/count-triplets-that-can-form-two-arrays-of-equal-xor/)

# Solution
* 维护一个前缀的异或和，可以在O(1)的时间复杂度内求得区间的异或和，然后枚举区间即可
* 时间复杂度O(n^3)

# Code
```cpp
class Solution {
public:
    int countTriplets(vector<int>& arr) {
        std::vector<int> x(arr.size() + 1, 0);
        x[0] = 0;
        for (int i = 1; i <= arr.size(); ++i) {
            x[i] = x[i - 1] ^ arr[i - 1];
        }
        
        int ans = 0;
        for (int i = 1; i <= arr.size(); ++i) {
            for (int j = i + 1; j <= arr.size(); ++j) {
                for (int k = j; k <= arr.size(); ++k) {
                    int lhs = x[j - 1] ^ x[i - 1];
                    int rhs = x[k] ^ x[j - 1];
                    if (lhs == rhs) ++ans;
                }
            }
        }
        return ans;
    }
};
```