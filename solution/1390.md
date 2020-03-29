# Problem
[Link](https://leetcode-cn.com/problems/four-divisors/)

# Solution

* 直接模拟
* 时间复杂度O(n * sqrt(n))

# Code
```cpp
class Solution {
public:
	int check(int x) {
		if (x == 1) return 0;
		int cnt = 0;
		int sum = 0;
		for (int i = 1; i * i <= x; ++i) {
			if (x % i == 0) {
				++cnt, sum += i;
				if (x / i != i) ++cnt, sum += (x / i);
			}

			if (cnt > 4) return 0;
		}

		return cnt == 4 ? sum : 0;
	}

	int sumFourDivisors(vector<int>& nums) {
		int ans = 0;
		for (int i = 0; i < nums.size(); ++i) {
			
			ans += check(nums[i]);
		}
		return ans;
	}
};
```