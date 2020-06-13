# Problem
[Link]()

# Solution
* 直接从前往后、从后往前分别做两次滑动窗口，用数组记录每一个前缀的最小数组长度、后缀最小数组长度，枚举断点即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
	int minSumOfLengths(vector<int>& nums, int target) {


		int n = nums.size();
		if (n <= 1) return -1;

		std::vector<int> pref(n, n + 1);
		std::vector<int> suff(n, n + 1);

		int L = 0;
		int sum = 0;
		for (int i = 0; i < nums.size(); ++i) {
			sum += nums[i];
			
			while (sum > target && L < i) {
				sum -= nums[L];
				++L;
			}

			if (sum == target) {
				pref[i] = std::min(pref[i], i - L + 1);
			}
		}

		int R = n - 1;
		sum = 0;
		for (int i = n - 1; i >= 0; --i) {
			sum += nums[i];
			
			while (sum > target && R > i) {
				sum -= nums[R];
				--R;
			}
			if (sum == target) {
				suff[i] = std::min(suff[i], R - i + 1);
			}
		}


		for (int i = 1; i < n; ++i) pref[i] = std::min(pref[i], pref[i - 1]);
		for (int i = n - 2; i >= 0; --i) suff[i] = std::min(suff[i], suff[i + 1]);
		int ans = n + n;
		for (int i = 0; i < n - 1; ++i) {
			ans = std::min(ans, pref[i] + suff[i + 1]);
		}
		return ans <= n ? ans : -1;
	}
};
```