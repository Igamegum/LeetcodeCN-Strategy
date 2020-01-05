
# Problem
[Link](https://leetcode-cn.com/problems/xor-queries-of-a-subarray/)

# Solution

* 维护前缀xor和即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    vector<int> xorQueries(vector<int>& arr, vector<vector<int>>& queries) {
        for (int i = 1; i < arr.size(); ++i) {
            arr[i] ^= arr[i - 1];
        }
        std::vector<int> ans;
        for (int i = 0; i < queries.size(); ++i) {
            int L = queries[i][0];
            int R = queries[i][1];
            int val = arr[R];
            if (L > 0) val ^= arr[L - 1];
            ans.push_back(val);
        }
        return ans;
    }
};
```