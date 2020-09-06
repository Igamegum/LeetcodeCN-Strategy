# Problem
[Link]()

# Solution
* 直接模拟，利用map维护数字的的出现数量，快速求出数量和
* 时间复杂度：O(n*logn)

# Code
```cpp
class Solution {
public:
    int calc(vector<int>& a, vector<int>& b) {
        int ans = 0;
        std::map<int, int> mp;
        for (int i = 0; i < b.size(); ++i) {
            ++mp[b[i]];
        }
        for (int i = 0; i < a.size(); ++i) {
            long long  lhs = (long long )a[i] * (long long )a[i];
            for (auto it = mp.begin(); it != mp.end(); ++it) {
                if ((lhs % it->first) != 0) continue;
                int rhs = lhs / it->first;
                
                if (rhs == it->first) {
                    int num = mp[it->first];
                    ans += (num) * (num - 1);
                } else {
                    if (mp.find(rhs) != mp.end()) ans += mp[rhs] * it->second;
                }
            }
        }
        return ans / 2;
    }
    int numTriplets(vector<int>& nums1, vector<int>& nums2) {
        
        int ans = 0;
        ans += calc(nums1, nums2);        
        ans += calc(nums2, nums1);
        return ans;
    }
};
```