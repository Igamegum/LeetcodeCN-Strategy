# Problem
[Link](https://leetcode-cn.com/problems/lucky-numbers-in-a-matrix/)

# Solution

* 数据范围很小，直接暴力即可
* O(n * m * (n + m))

# Code
```cpp
class Solution {
public:
    bool check(vector<vector<int>>& matrix, int r, int c) {
        int n = matrix.size();
        int m = matrix[0].size();
        for (int i = 0; i < n; ++i) {
            if (i != r && matrix[i][c] > matrix[r][c]) return false;
        }
        
        for (int i = 0; i < m; ++i) {
            if (i != c && matrix[r][i] < matrix[r][c]) return false;
        }
        
        return true;
    }
    vector<int> luckyNumbers (vector<vector<int>>& matrix) {
        std::vector<int> ans;
        if (matrix.size() < 1) return ans;
        
        
        for (int i = 0; i < matrix.size(); ++i) {
            for (int j = 0; j < matrix[i].size(); ++j) {
                if (check(matrix, i, j)) {
                    ans.push_back(matrix[i][j]);
                }
            }
        }
        
        return ans;
    }
};
```