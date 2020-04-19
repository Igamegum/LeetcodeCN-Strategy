# Problem
[Link](https://leetcode-cn.com/problems/ju-qing-hong-fa-shi-jian/)

# Solution

* 分别维护C、R、H的前缀和，然后对于每个requirements，分别二分查找能满足的天数，取最大值即可
* 时间复杂度O(n * logm)

# Code
```cpp
class Solution {
public:
    vector<int> getTriggerTime(vector<vector<int>>& increase, vector<vector<int>>& requirements) {
        int n = increase.size();
        std::vector<int> C(n, 0);
        std::vector<int> R(n, 0);
        std::vector<int> H(n, 0);
        for (int i = 0; i < increase.size(); ++i) {
            if (i == 0) {
                C[i] = increase[i][0];
                R[i] = increase[i][1];
                H[i] = increase[i][2];
            } else {
                C[i] = increase[i][0] + C[i - 1];
                R[i] = increase[i][1] + R[i - 1];
                H[i] = increase[i][2] + H[i - 1];
            }
        }
        
        std::vector<int> ans;
        for (int i = 0; i < requirements.size(); ++i) {
            int c = requirements[i][0];
            int r = requirements[i][1];
            int h = requirements[i][2];
            
            int dc = std::lower_bound(C.begin(), C.end(), c) - C.begin();
            ++dc;
            if (c <= 0) dc = 0;
            
            int dr = std::lower_bound(R.begin(), R.end(), r) - R.begin();
            ++dr;
            if (r <= 0) dr = 0;
            
            int dh = std::lower_bound(H.begin(), H.end(), h) - H.begin();
            ++dh;
            if (h <= 0) dh = 0;
            
            int d = std::max(dc, std::max(dr, dh));
            if (d > n) d = -1;
            ans.push_back(d);
            
        }
        
        return ans;
    }
};
```