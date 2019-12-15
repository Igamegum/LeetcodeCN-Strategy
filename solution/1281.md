# Problem
[Link](https://leetcode-cn.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/)

# Solution

* 略
* 时间复杂度O(len(n))

# Code
```cpp
class Solution {
public:
    int subtractProductAndSum(int n) {
        long long sum = 0;
        long long x = 1;
        while (n) {
            x *= (n % 10);
            sum += (n % 10);
            n /= 10;
        }
        return x - sum;
    }
};
```