# Problem
[Link](https://leetcode-cn.com/problems/maximum-number-of-non-overlapping-subarrays-with-sum-equals-target/)

# Solution
* 记录每种前缀和出现的位置，然后统计答案
* 时间复杂度：O(n*n)

# Code
```cpp
class Solution {
public:
    struct Line {
        int L;
        int R;
        Line (int l, int r) {
            L = l;
            R = r;
        }
        const bool operator < (const Line& T) const {
            if (R == T.L) return L < T.L;
            return R < T.R;
        }
    };
    
    int maxNonOverlapping(vector<int>& nums, int target) {
        std::vector<Line> lines;
        std::map<int, std::vector<int>> mp;
        mp[0].push_back(-1);
        int sum = 0;
        int ans = 0;
        int max_r = -1;
        for (int i = 0; i < nums.size(); ++i) {
            sum += nums[i];
            int val = sum - target;
            if (mp.find(val) != mp.end()) {
                for (int j = mp[val].size() - 1; j >= 0; --j) {
                    if (mp[val][j] + 1 > max_r && i > max_r) {
                        ++ans;
                        max_r = i;
                    } else {
                        break;
                    }
                }
            }
                mp[sum].push_back(i);    
        }

        return ans;
    }
};
```