# Problem
[Link](https://leetcode-cn.com/problems/find-the-minimum-number-of-fibonacci-numbers-whose-sum-is-k/)

# Solution

* 首先维护一个斐波那契数组，然后贪心取最大值即可，取最大值可以二分
* 时间复杂度O(logk)

# Code
```cpp
class Solution {
public:
    
    int findMinFibonacciNumbers(int k) {
        std::vector<long long>  num;
        num.push_back(1);
        num.push_back(1);
        while (true) {
            int n = num.size();
            long long val = num[n - 1] + num[n - 2];
            num.push_back(val);
            if (val >= 1e9) break;
        }
        
        int ans = 0;
        while (k) {
            int id = std::lower_bound(num.begin(), num.end(), k) - num.begin();
            int st = num[id] == k ? id : id - 1;
            k -= num[st];
            ++ans;
        }
        return ans;
    }
};
```