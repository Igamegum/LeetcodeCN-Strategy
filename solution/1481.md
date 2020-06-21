# Problem
[Link](https://leetcode-cn.com/problems/least-number-of-unique-integers-after-k-removals/)

# Solution
* 统计每个数字出现的次数，优先删除出现次数小的数字
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    int findLeastNumOfUniqueInts(vector<int>& arr, int k) {
        std::map<int, int> mp;
        for (int i = 0; i < arr.size(); ++i) {
            ++mp[arr[i]];
        }
        typedef std::pair<int, int> PII;
        std::vector<PII> nums;
        for (auto it = mp.begin(); it != mp.end(); ++it) {
            nums.push_back( std::make_pair(it->second, it->first) );
        }
        std::sort(nums.begin(), nums.end());
        int ans = nums.size();
        for (int i = 0; i < nums.size(); ++i) {
            if (k >= nums[i].first) {
                --ans;
                k-= nums[i].first;
            } else {
                break;
            }
            
        }
        return ans;
    }
};
```