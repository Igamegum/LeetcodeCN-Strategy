# Problem
[Link]()

# Solution
* 直接模拟
* 时间复杂度：O(1)

# Code
```cpp
class Solution {
public:
    int countOdds(int low, int high) {
        int diff = high - low;
        int ans = 0;
        if (low & 1) {
            ans = diff / 2 + 1;
        } else {
            ans = (diff + 1) / 2;
        }
        return ans;
    }
};
```