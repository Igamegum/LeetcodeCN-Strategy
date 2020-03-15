# Problem
[Link](https://leetcode-cn.com/problems/maximum-performance-of-a-team/)

# Solution

* 首先，将成员按照efficiency从大到小排序。
* 枚举当前成员，以其efficiency作为所选团队的最小 efficiency，那么只需要在 efficiency 比当前成员大的成员中，选取K - 1个成员，使其 speed的和最大即可，这步可以用优先队列维护
* 时间复杂度O(n * logn)

# Code
```cpp
class Solution {
public:
	struct Node{
		int spd;
		int eff;

		Node(int sp, int ef) {
			spd = sp;
			eff = ef;
		}
		const bool operator < (const Node &T) const {
			if (eff != T.eff) return eff > T.eff;
			return spd > T.spd;
		}
	};

	int maxPerformance(int n, vector<int>& speed, vector<int>& efficiency, int k) {
		long long Mod = 1e9 + 7;
		std::vector<Node> nodes;
		
		for (int i = 0; i < n; ++i) {
			nodes.push_back(Node(speed[i], efficiency[i]));
		}
		std::sort(nodes.begin(), nodes.end());

		std::priority_queue<int, vector<int>, std::greater<int>> q;
		long long sum = 0;

		long long ans = 0;
		for (int i = 0; i < n; ++i) {
			long long sum_spd = sum + nodes[i].spd;
			ans = std::max(ans, sum_spd * nodes[i].eff);
			q.push(nodes[i].spd); 
			sum += nodes[i].spd;
			while (q.size() > k - 1) {
				sum -= q.top();
				q.pop();
			}
		}

		return ans % Mod;

	}
};
```