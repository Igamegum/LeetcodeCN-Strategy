# Problem
[Link](https://leetcode-cn.com/problems/build-an-array-with-stack-operations/)

# Solution
* 直接模拟
* 时间复杂度O(n),空间复杂度O(n)

# Code
```cpp
class Solution {
public:
    vector<string> buildArray(vector<int>& target, int n) {
        std::vector<string> ans;
        int id = 0;
        for (int i = 1; i <= n; ++i) {
            if (id == target.size()) break;
            if (i == target[id]) {
                ans.push_back("Push");
                ++id;
            } else {
                ans.push_back("Push");
                ans.push_back("Pop");
            }
        }
        
        return ans;
    }
};
```