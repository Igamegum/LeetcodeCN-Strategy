# Problem
[Link](https://leetcode-cn.com/problems/sum-of-mutated-array-closest-to-target/)

# Solution

* 直接二分答案即可,注意答案可能为0
* 时间复杂度O(nlog(1e5))

# Code
```cpp
class Solution {
public:
    int findBestValue(vector<int>& arr, int target) {
        int L = 0;
        int R = target;
        int min_diff = 1e5;
        int ans = 1e5;
        while (L <= R) 
        {
            int sum = 0;
            int mid = (L + R) >> 1;
            for (int i = 0; i < arr.size(); i++) {
                sum += std::min(arr[i], mid);
            }
            int diff = std::abs(sum - target);
            if (diff < min_diff || (diff == min_diff && mid < ans)) {
                min_diff = diff;
                ans = mid;
            }
            int val = sum - target;
            if (val == 0) {
                break;
            } else if (val > 0) {
                R = mid - 1;
            } else {
                L = mid + 1;
            }
        }
        return ans;
    }
};
```