# Problem
[Link](https://leetcode-cn.com/problems/count-servers-that-communicate/)

# Solution

* 直接分别标记每一行，每一列上，服务器的数量，如果某一行（某一列）上的服务器的数量大于 1 ，那么这一行（这一列）上的服务器都能通信
* 时间复杂度O(n * m)

# Code
```cpp
class Solution {
public:
    int countServers(vector<vector<int>>& grid) {
        if (grid.size() <= 0 || grid[0].size() <= 0) return 0;
        
        std::vector<int> row(grid.size(), 0);
        std::vector<int> col(grid[0].size(), 0);
        
        for (int i = 0; i < grid.size(); ++i) {
            for (int j = 0; j < grid[i].size(); ++j) {
                if (grid[i][j] == 1) {
                    ++row[i];
                    ++col[j];    
                }
                
            }
        }
        
        int ans = 0;
        for (int i = 0; i < grid.size(); ++i) {
            for (int j = 0; j < grid[i].size(); ++j) {
                if (grid[i][j] ) {
                    if (row[i] > 1 || col[j] > 1) {
                        ++ans;
                    }
                }
            }
        }
        
        return ans;
      
    }
};
```