# Problem
[Link](https://leetcode-cn.com/problems/minimum-time-to-collect-all-apples-in-a-tree/)

# Solution
* 如果某个节点的子树下都没有苹果，那么这个节点是不需要到达的。考虑从节点i出发，到有苹果的节点j，那么显然对于i子树来说，花费是点i到点j的距离*2
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    
	bool vis[100100];
	std::map<int, std::vector<int> > E;

	int dfs(const int root, const vector<bool>& hasApple) {
		int sum = 0;

		for (int i = 0; i < E[root].size(); ++i) {
			int id = E[root][i];
			if (!vis[id]) {
				vis[id] = true;
				sum += dfs(id, hasApple);
			}
		}
		int ans = 0;
		if (sum > 0) {
			ans = sum;
			if (root != 0) ++ans;
		} else  if (hasApple[root]) {
			ans = 1;
		}
		//std::cout << root << "  " << ans << std::endl;
		return ans;
		
		
	}

	int minTime(int n, vector<vector<int>>& edges, vector<bool> hasApple) {
		memset(vis, false, sizeof(vis));
		E.clear();
		for (int i = 0; i < edges.size(); ++i) {
			E[edges[i][0]].push_back(edges[i][1]);
			E[edges[i][1]].push_back(edges[i][0]);
		}
		vis[0] = true;
		int res = dfs(0, hasApple);
		return res * 2;
	}
};
```