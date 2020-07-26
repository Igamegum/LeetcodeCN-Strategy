# Problem
[Link]()

# Solution
* 由于灯泡的初始状态为0，所以第一段连续的0是不需要操作的区间，从第一个1开始到最后一个数字是需要操作的区间
* 直接统计有多少个不同的0,1段的数量就行
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    int minFlips(string target) {
        
        int n = target.size();
        int st = n;
        for (int i = 0; i < n; ++i) {
            if (target[i] != '0') {
                st = i;
                break;
            }
        }
        int prev = '0';
        int ans = 0;
        for (int i = st; i < n ; ++i) {
            if (target[i] != prev) {
                ++ans;
                prev = target[i];
            }
        }
        return ans;
    }
};
```