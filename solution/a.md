# Problem
[Link](https://leetcode-cn.com/problems/most-visited-sector-in-a-circular-track/)

# Solution
* 直接
* 时间复杂度：O(n*m)

# Code
```cpp
class Solution {
public:
    vector<int> mostVisited(int n, vector<int>& rounds) {
        std::vector<int> ans;
        std::vector<int> sum(n + 1, 0);
        int cur = rounds[0];
        ++sum[cur];
        for (int i = 1; i < rounds.size(); ++i) {
            for (int j = cur + 1; ; ++j) {
                if (j > n) j = 1;
                ++sum[j];
                if (j == rounds[i]) {
                    cur = rounds[i];
                    break;
                }
            }
        }
        int max_siz = 0;
        for (int i = 0; i < sum.size(); ++i) {
            max_siz = std::max(max_siz, sum[i]);
        }
        for (int i = 0; i < sum.size(); ++i) {
            if (sum[i] == max_siz) {
                ans.push_back(i);
            }
        }
        return ans;
    }
};
```