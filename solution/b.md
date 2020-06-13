# Problem
[Link](https://leetcode-cn.com/problems/subrectangle-queries/)

# Solution
* 直接暴力
* 时间复杂度O(n*n)

# Code
```cpp
class SubrectangleQueries {
public:
    vector<vector<int>> rectangle;
    SubrectangleQueries(vector<vector<int>>& rectangle) {
        this->rectangle = rectangle;
    }
    
    void updateSubrectangle(int row1, int col1, int row2, int col2, int newValue) {
        for (int i = row1; i <= row2; ++i) {
            for (int j = col1; j <= col2; ++j) {
                rectangle[i][j] = newValue;
            }
        }
    }
    
    int getValue(int row, int col) {
        return rectangle[row][col];
    }
};
```