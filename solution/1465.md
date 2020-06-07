# Problem
[Link](https://leetcode-cn.com/problems/maximum-area-of-a-piece-of-cake-after-horizontal-and-vertical-cuts/)

# Solution
* 排序后，分别取分割的h和w的最大值即可
* 时间复杂度O(nlogn)
# Code
```cpp
class Solution {
public:
    int maxArea(int h, int w, vector<int>& horizontalCuts, vector<int>& verticalCuts) {
        int max_w = 0;
        horizontalCuts.push_back(h);
        verticalCuts.push_back(w);
        std::sort(horizontalCuts.begin(), horizontalCuts.end());
        std::sort(verticalCuts.begin(), verticalCuts.end());
        
        for (int i = 0; i < verticalCuts.size(); ++i) {
            if (i == 0) {
                max_w = std::max(max_w, verticalCuts[i] - 0);
            } else {
                max_w = std::max(max_w, verticalCuts[i] - verticalCuts[i - 1]);
            }
        }
        long long  ans = 0; 
        const int mod = 1e9 + 7;
        long long area;
        for (int i = 0; i < horizontalCuts.size(); ++i) {
            area = 0;
            if (i == 0) {
                area = static_cast<long long>(horizontalCuts[i]) * static_cast<long long>(max_w);
            } else {
                area = (static_cast<long long>(horizontalCuts[i]) - static_cast<long long>(horizontalCuts[i - 1])) * static_cast<long long>(max_w);
            }
            ans = std::max(ans, area);
        }
        
        return ans % mod;
    }
};
```