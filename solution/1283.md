# Problem
[Link](https://leetcode-cn.com/problems/find-the-smallest-divisor-given-a-threshold/)

# Solution

* 直接二分答案即可
* 时间复杂度O(n * log(1e6))

# Code
```cpp
class Solution {
public:
    int smallestDivisor(vector<int>& nums, int threshold) {
        int L = 1;
        int R = 1e6;
        int ans = 1e6;
        while (L <= R) {
            int mid = (L + R) >> 1;
            int sum = 0;
            for (int i = 0; i < nums.size(); ++i) {
                sum += nums[i] / mid;
                if (nums[i] % mid) ++sum;
            }
            
            if (sum <= threshold) {
                ans = std::min(ans, mid);
                R = mid - 1;
            } else {
                L = mid + 1;
            }
        }
        return ans;
    }
};
```