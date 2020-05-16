# Problem
[Link]()

# Solution
* 首先，位数多的数字一定更大，那么不妨设len[i]代表花费为i所能选取的数字的最大长度，那么显然有len[i] = max(len[i - cost[j]]){ 0 <= j < 9}
* 确立好数位的长度之后，接下来只要贪心取数字大的即可
* 时间复杂度O(n * 9)

# Code
```cpp

class Solution {
public:
    
	string largestNumber(vector<int>& cost, int target) {
		std::vector<int> len(target + 1, -1);
		len[0] = 0;
		for (int i = 1; i <= target; ++i) {
			int max_len = -1;
			for (int j = cost.size() - 1; j >= 0; --j) {
				if (i - cost[j] >= 0 && len[i - cost[j]] >= 0) {
					max_len = std::max(max_len, len[i - cost[j]] + 1);
				}
			}
			len[i] = max_len;
		}
		if (len[target] < 0) return "0";
		std::string ans;
		while (target) {
			for (int i = cost.size() - 1; i >= 0; --i) {
				if (target - cost[i] >= 0 && len[target] == len[target - cost[i]] + 1) {
					ans += to_string(i + 1);
					target -= cost[i];
					break;
				}
			}
		}
		return ans;
	}
};
```