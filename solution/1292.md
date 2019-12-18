# Problem
[Link](https://leetcode-cn.com/problems/maximum-side-length-of-a-square-with-sum-less-than-or-equal-to-threshold/)

# Solution

* 这题本质同[1277](https://leetcode-cn.com/problems/count-square-submatrices-with-all-ones/),直接维护二维矩阵的元素和，然后枚举矩阵即可
* 时间复杂度O(n * m)

# Code
```cpp
class Solution {
public:
    int countSquares(vector<vector<int>>& matrix) {
        
        for (int i = 0; i < matrix.size(); ++i) {
            for (int j = 0; j < matrix[i].size(); ++j) {
                int pup = (i == 0) ? 0 : matrix[i - 1][j];
                int plf = (j == 0) ? 0 : matrix[i][j - 1];
                int pff = (i == 0 || j == 0) ? 0  : matrix[i - 1][j - 1];
                matrix[i][j] = matrix[i][j] + pup + plf - pff;
            }
        }
        
        int ans = 0;
        for (int i = 0; i < matrix.size(); ++i) {
            for (int j = 0; j < matrix[i].size(); ++j) {
                for (int k = 1;;k++) {
                    int x = i + k - 1;
                    int y = j + k - 1;
                    if (x >= matrix.size() || y >= matrix[i].size()) {
                        break;
                    }
                    int a = matrix[x][y];
                    int b = (j == 0) ? 0 : matrix[x][j - 1];
                    int c = (i == 0) ? 0 : matrix[i - 1][y];
                    int d = (i == 0 || j == 0) ? 0 : matrix[i - 1][j - 1];
                    int sum = a - b - c + d;
                    if (sum == k * k) ++ans;
                }
            }
        }
        return ans;
    }
};
```