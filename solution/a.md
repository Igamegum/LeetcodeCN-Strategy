# Problem
[Link]()

# Solution
* 直接模拟
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    bool threeConsecutiveOdds(vector<int>& arr) {
        int cnt = 0;
        for (int i = 0; i < arr.size(); ++i) {
            if (arr[i] & 1) {
                ++cnt;
                if (cnt >= 3) return true;
            } else {
                cnt = 0;
            }
        }
        return false;
    }
};
```