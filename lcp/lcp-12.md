# Problem
[Link](https://leetcode-cn.com/problems/xiao-zhang-shua-ti-ji-hua/)

# Solution

* 直接二分答案
* 时间复杂度O(nlog1e9)

# Code
```cpp
class Solution {
public:
    bool check(const vector<int>& time, int m, int max_val) {

        int sum = 0;
        int mx = 0;
        int day = 1;
        for (int i = 0; i < time.size(); ++i) {
            mx = std::max(mx, time[i]);
            sum += time[i];
            if (sum - mx > max_val) {
                ++day;
                sum = time[i];
                mx = time[i];
            }
        }
        return day <= m;

    }
    int minTime(vector<int>& time, int m) {
        int L = 0;
        int sum = 0;
        for (int i = 0; i < time.size(); ++i) sum += time[i];
        //std::sort(time.begin(), time.end());
        int R = sum;
        int ans = sum;
        while (L <= R) {
            int mid = (L + R) >> 1;
            if (check(time, m, mid)) {
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