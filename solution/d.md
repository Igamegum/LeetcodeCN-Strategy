# Problem
[Link](https://leetcode-cn.com/problems/number-of-ways-of-cutting-a-pizza/)

# Solution
* 记忆化搜索或DP均可
* 不妨设立dp数组，dp[sx][sy][ex][ey][k]代表子矩阵左上角坐标为(sx, sy),右下角坐标为(ex, ey),切分成k块的方案数。显然，枚举水平切分的位置和垂直切分的位置，累加其方案数即可。
* dp[sx][sy][ex][ey] = sum(dp[i][sy][ex][ey]) + sum(dp[sx][j][ex][ey]) {i = sx + 1...ex, j = sy + 1...ey}
* 特别的，此时的空间复杂度为O(n^4)，注意到ex, ey恒为原始矩阵的右下角，不会改变，所以我们可以省略ex, ey 这两维的状态，那么状态记为 dp[sx][sy][k]
* 另外，为了快速求出子矩阵[sx][sy][ex][ey]的苹果数，可以考虑维护一个二维的前缀和apple[x][y],代表的是从点(1, 1)到点(x, y)的苹果总数，那么根据容斥原理，可以在O(1)的时间复杂度内求出任意子矩阵的苹果总数
* sum[sx][sy][ex][ey] = apple[ex][ey] - apple[ex][sy - 1] - apple[sx - 1][ey] + apple[sx - 1][sy - 1]
* 时间复杂度O(n^3)

# Code
```cpp
class Solution {
public:
	int status[52][52][12];

	int n;
	int m;
	int apple[52][52];
	const int Mod = 1e9 + 7;

	long long dfs(const int sx, const int sy, const int ex, const int ey, int k) {
		//std::cout << sx << " " << sy << " " << ex << " " << ey << " " << k << std::endl;
		if (status[sx][sy][k] != -1) return status[sx][sy][k];
		if (k == 1) {
			status[sx][sy][k] = 1;
			return 1;
		}
		long long sum = 0;
		int total_apple = apple[ex][ey] - apple[ex][sy - 1] - apple[sx - 1][ey] + apple[sx - 1][sy - 1];
		//enum row
		for (int i = sx; i <= ex - 1; ++i) {
			int up = apple[i][ey] - apple[i][sy - 1] - apple[sx - 1][ey] + apple[sx - 1][sy - 1];
			int down = total_apple - up;
			if (up > 0 && down >= k - 1) {
				sum += dfs(i + 1, sy, ex, ey, k - 1);
				sum %= Mod;
			}
		}

		//enum col
		for (int j = sy; j <= ey - 1; ++j) {
			int left = apple[ex][j] - apple[ex][sy - 1] - apple[sx - 1][j] + apple[sx - 1][sy - 1];
			int right = total_apple - left;
			if (left > 0 && right >= k - 1) {
				sum += dfs(sx, j + 1, ex, ey, k - 1);
				sum %= Mod;
			}
		}
		status[sx][sy][k] = sum;
		return sum;
	}


	int ways(vector<string>& pizza, int k) {
		memset(status, -1, sizeof(status));
		memset(apple, 0, sizeof(apple));

		n = pizza.size();
		m = pizza[0].size();

		//init apple sum
		for (int i = 1; i <= pizza.size(); ++i) {
			for (int j = 1; j <= pizza[i - 1].size(); ++j) {
				char a = pizza[i - 1][j - 1];
				apple[i][j] = apple[i - 1][j] + apple[i][j - 1] - apple[i - 1][j - 1];
				if (a == 'A') apple[i][j] += 1;
			}
		}

		long long  ans = dfs(1, 1, n, m, k);
		return ans;

	}
};
```