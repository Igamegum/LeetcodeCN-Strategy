# Problem
[Link](https://leetcode-cn.com/problems/replace-elements-with-greatest-element-on-right-side/)

# Solution

* 从后往前维护最大值即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    vector<int> replaceElements(vector<int>& arr) {
        int max_val = -1;
        for (int i = arr.size() - 1; i >= 0; --i) {
            int temp = max_val;
            max_val = std::max(max_val, arr[i]);
            arr[i] = temp;
        }
        return arr;
    }
};
```