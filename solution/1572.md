# Problem
[Link](https://leetcode-cn.com/problems/matrix-diagonal-sum/)

# Solution
* 直接模拟
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    int diagonalSum(vector<vector<int>>& mat) {
        int sum = 0;
        for (int i = 0; i < mat.size(); ++i) {
            sum += mat[i][i];
            if (mat.size() - 1 - i != i)sum += mat[i][mat.size() - 1 - i];   
        }
        return sum;
    }
};
```