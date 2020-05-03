# Problem
[Link](https://leetcode-cn.com/problems/qi-wang-ge-shu-tong-ji/)

# Solution

* 显然，根据期望的可加性质，对每个不同的数值分开求期望即可。又因为每个数值，不管数量又多少，其期望都是1，所以本题就变成求不同数值的数量
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    int expectNumber(vector<int>& scores) {
        std::set<int> s;
        for (int i = 0; i < scores.size(); ++i) {
            s.insert(scores[i]);
        }
        return s.size();
        
    }
};
```