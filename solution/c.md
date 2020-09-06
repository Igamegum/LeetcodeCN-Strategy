# Problem
[Link](https://leetcode-cn.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/)

# Solution
* 直接二分答案，然后再O(n)的时间复杂度进行check
* check相当于有一个固定大小为k的删除窗口，将数组分为前后两个部分，这两个部分可以利用后缀和的方式，快速得到能否满足单调不递减的性质
* 时间复杂度：O(n*logn)

# Code
```cpp
class Solution {
public:
    bool check(vector<int>& arr, vector<int>& suff, vector<bool>& can, const int k) {
        if (k >= arr.size()) return true;
        int pre_max = 0;
        for (int i = 0; i < arr.size(); ++i) {
			
			if (i + k >= arr.size()) return true;
			int rhs = suff[i + k];
			//cout << i << "  " << pre_max << "  " << rhs << "  " << can[i + k + 1] << "  " << k << endl;
			if (rhs >= pre_max && can[i + k]) return true;
            if (arr[i] < pre_max) return false;
            pre_max = std::max(pre_max, arr[i]);
            
        }
        return false;
        
    }
    int findLengthOfShortestSubarray(vector<int>& arr) {
        int n = arr.size();
        std::vector<int> suff(n, arr[n - 1]);
        std::vector<bool> can(n, true);
        for (int i = n - 2; i >= 0; --i) {
            suff[i] = std::min(suff[i + 1], arr[i]);
            if (!can[i + 1] || suff[i + 1] < arr[i]) {
                can[i] = false;
            }
        }
        
        int L = 0;
        int R = n - 1;
        int ans = R;
        while (L <= R) {
            int mid = (L + R) >> 1;
            if (check(arr, suff, can, mid)) {
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