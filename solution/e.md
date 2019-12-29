
# Problem
[Link](https://leetcode-cn.com/problems/find-n-unique-integers-sum-up-to-zero/)

# Solution

* 这题有很多种构造方法，直接根据N的大小，存一正一反的数字即可。
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    vector<int> sumZero(int n) {
        std::vector<int> ans;
        if (n & 1) {
            --n;
            ans.push_back(0);
        }
        for (int i = 1; i <= n / 2; ++i) {
            ans.push_back(i);
            ans.push_back(i * -1);
        }
        return ans;
    }
};
```