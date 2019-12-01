# Problem
[Link](https://leetcode-cn.com/problems/count-square-submatrices-with-all-ones/)

# Solution
* 容斥原理
* 由于数据范围比较小，直接枚举正方形的左上角点，和右下角点，确立矩形的范围，只要举矩形内的值的和等于矩形的大小，那么这个矩形就是所求的子矩形
* 问题在于怎么快速求的子矩形的元素和。考虑维护二维前缀和 sum[i][j], sum[i][j] 表示 累加和(x = 1 ~ i, y = 1 ~ j)
* 对于子矩形，假定左上角坐标为(i, j),右下角坐标为 (x, y),那么这个子矩形的元素和等于 sum[x][y] - sum[x][j - 1] - sum[i - 1][y] + sum[i - 1][j - 1]

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