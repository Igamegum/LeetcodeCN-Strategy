# Problem
[Link]()

# Solution
* 智商题，考虑维护一个前缀最大值，表示这个连续需要的操作次数。
* 如果当前数字大于前缀最大值，那么操作次数需要增加 target[i] - target[i - 1]。举个例子，3,2,5，对于5来说，虽然前缀最大值是3，但是能贡献给5的，只有target[i - 1]次，也即是2次，需要再额外操作3次
* 如果当前数字没有前缀最大值，并且当前数字大于前一个数字，那么操作数也不能连续，需要增加 target[i] - target[i - 1]次
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    int minNumberOperations(vector<int>& target) {
        int n = target.size();
        int ans   = target[0];
        int max_v = target[0];
        for (int i = 1; i < n; ++i) {
            if (target[i] > max_v) {
                ans += target[i] - target[i - 1];
                max_v = max(target[i], max_v);
            } else if (target[i] <= max_v  && target[i] > target[i - 1]) {
                ans += target[i] - target[i - 1];
                max_v = target[i];
            }
        }
        return ans;
    }
};
```