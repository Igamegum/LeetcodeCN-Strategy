# Problem
[Link](https://leetcode-cn.com/problems/kids-with-the-greatest-number-of-candies/)

# Solution

* 直接跟最大值比较即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    vector<bool> kidsWithCandies(vector<int>& candies, int extraCandies) {
        std::vector<bool> ans;
        int max_val = 0;
        for (int i = 0; i < candies.size(); ++i) {
            max_val = std::max(max_val, candies[i]);
        }
        
        for (int i = 0; i < candies.size(); ++i) {
            if (candies[i] + extraCandies >= max_val) {
                ans.push_back(true);
            } else {
                ans.push_back(false);
            }
        }
        
        return ans;
    }
    
};
```