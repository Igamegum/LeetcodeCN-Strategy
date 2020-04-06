# Problem
[Link](https://leetcode-cn.com/problems/count-largest-group/)

# Solution

* 直接map模拟即可
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    int calc(int n) {
        int sum = 0;
        while (n) {
            sum += n % 10;
            n /= 10;
        }
        return sum;
    }
    
    int countLargestGroup(int n) {
        std::map<int, int> mp;
        for (int i = 1; i <= n; ++i) ++mp[calc(i)];
            
        int max_cnt = 0;
        int ans = 0;
        for (auto it = mp.begin(); it != mp.end(); ++it) {
            if (it->second > max_cnt) {
                max_cnt = it->second;
                ans = 1;
            } else if (it->second == max_cnt) {
                ++ans;
            }
        }
            
        
        return ans;
    }
};
```