# Problem
[Link](https://leetcode-cn.com/problems/final-prices-with-a-special-discount-in-a-shop/)

# Solution
* 数据范围小，直接暴力的O(n^2)可解
* 维护一个单调上升的栈，时间复杂度可以做到O(n)
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    vector<int> finalPrices(vector<int>& prices) {
        int n = prices.size();
        std::vector<int> ans(n, 0);
        std::stack<int> S;
        for (int i = 0; i < prices.size(); ++i)  {
            
            while (S.size() && prices[i] <= prices[S.top()]) {
                ans[S.top()] = prices[S.top()] - prices[i];
                S.pop();
            }
            S.push(i);
        }

        while (!S.empty()) {
            ans[S.top()] = prices[S.top()];
            S.pop();
        }

        return ans;
    }
};
```