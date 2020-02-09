# Problem
[Link](https://leetcode-cn.com/problems/check-if-n-and-its-double-exist/)

# Solution

* 注意数字为0的时候，需要有多个
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    bool checkIfExist(vector<int>& arr) {
        std::map<int, int> mp;
        for (int i = 0; i < arr.size(); ++i) {
            ++mp[arr[i]];
        }
        for (int i = 0; i < arr.size(); ++i) {
            if ((arr[i] == 0 && mp[arr[i]] > 1) || (mp.find(arr[i] * 2) != mp.end() && arr[i] != 0))  {
                return true;
            }
        }
        return false;
    }
};
```