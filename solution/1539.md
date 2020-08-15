# Problem
[Link](https://leetcode-cn.com/problems/kth-missing-positive-number/)

# Solution
* 直接set存储所有数组中的元素，然后暴力枚举答案
* 时间复杂度：O(n*logn)

# Code
```cpp
class Solution {
public:
    int findKthPositive(vector<int>& arr, int k) {
        std::set<int> S;
        for (int i = 0; i < arr.size(); ++i) S.insert(arr[i]);
        int cnt = 0;
        for (int i = 1; ; ++i) {
            if (S.find(i) == S.end()) {
                ++cnt;
                if (cnt == k) return i;
            }
        }
        return -1;
    }
};

```