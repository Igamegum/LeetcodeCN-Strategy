# Problem
[Link]()

# Solution
* 维护前后缀，枚举切割点
* 时间复杂度O(n)

# Code
```cpp

class Solution {
public:
	int numSubmat(vector<vector<int>>& mat) {
		int n = mat.size();
		int m = mat[0].size();
        for (int i = 0; i < n; ++i) {
            for (int j = 1; j < m; ++j) {
                mat[i][j] += mat[i][j - 1];
            }
        }
        
        int ans = 0;
        for (int L = 0; L < m; ++L) {
            for (int R = L; R < m; ++R) {
                int cnt = 0;
                for (int r = 0; r < n; ++r) {
                    int sum = L - 1 >= 0 ? mat[r][R] - mat[r][L - 1] : mat[r][R];
                    cnt = sum != R - L + 1 ? 0 : cnt + 1;
                    ans += (cnt);
                }
            }
        }
        return ans;
	}
};
```