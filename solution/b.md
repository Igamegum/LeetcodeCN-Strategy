# Problem
[Link](https://leetcode-cn.com/problems/divide-array-in-sets-of-k-consecutive-numbers/)

# Solution

* 对原数组排序后，直接取最小的元素开始模拟即可。
* 时间复杂度O(n * logn)

# Code
```cpp
class Solution {
public:
    bool isPossibleDivide(vector<int>& nums, int k) {
        if (nums.size() % k) return false;
    
        std::multiset<int> S;
        for (int i = 0; i < nums.size(); ++i) {
            S.insert(nums[i]);
        }
        
        while (S.size()) {
            auto is = S.begin();
            int st = *is;
            S.erase(is);
            
            for (int i = 1; i <= k - 1; ++i) {
                auto it = S.find(st + i);
                if (it == S.end()) return false;                
                S.erase(it);
            }
        }
        
        return true;
    }
};
```