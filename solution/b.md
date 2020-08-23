# Problem
[Link](https://leetcode-cn.com/problems/maximum-number-of-coins-you-can-get/)

# Solution
* 排序后直接模拟从两段取，从最小端取一堆，从最大端取连续的两堆
* 时间复杂度：O(nlogn)

# Code
```cpp
class Solution {
public:
    int maxCoins(vector<int>& piles) {
        std::sort(piles.begin(), piles.end());
        int L = 0;
        int R = piles.size() - 1;
        int ans = 0;
        while (L < R) {
            ans += piles[R - 1];
            ++L;
            R -= 2;
        }
        return ans;
    }
};
```