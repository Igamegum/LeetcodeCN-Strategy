# Problem
[Link](https://leetcode-cn.com/problems/can-make-arithmetic-progression-from-sequence/)

# Solution
* 直接模拟
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    bool canMakeArithmeticProgression(vector<int>& arr) {
        std::sort(arr.begin(), arr.end());
        bool can = true;
        for (int i = 2; i < arr.size(); ++i) {
            if (arr[i] - arr[i - 1] != arr[i - 1] - arr[i - 2]) {
                can = false;
                break;
            }
        }
        return can;
    }
};
```