# Problem
[Link](https://leetcode-cn.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/)

# Solution
* flyod
* 由于n只有100，直接flyod求出任意两点之间的最短距离，然后按照题意求出答案
* 时间复杂度O(n * n * n)

# Code
```cpp
class Solution {
public:
    int dist[110][110];
    const int max_dist = 0x3f3f3f3f;
    int findTheCity(int n, vector<vector<int>>& edges, int distanceThreshold) {
        
        
        for (int i = 0; i <= n + 5; ++i) {
            for (int j = 0; j <= n + 5; ++j) {
                dist[i][j] =  i == j ? 0 : max_dist;
            }
        }
        
        
        for (int i = 0; i < edges.size(); ++i) {
            dist[edges[i][0]][edges[i][1]] = std::min(edges[i][2], dist[edges[i][0]][edges[i][1]]);
            dist[edges[i][1]][edges[i][0]] = std::min(edges[i][2], dist[edges[i][1]][edges[i][0]]);
        }
        
        //Flyod
        for (int k = 0; k < n; ++k) {
            for (int i = 0; i < n; ++i) {
                for (int j = 0; j < n; ++j) {
                    dist[i][j] = std::min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }
        
        int min_num = n + 1;
        int ans = n;
        for (int i = n - 1; i >= 0; --i) {
            int num = 0;
            for (int j = 0; j < n; ++j) {
                if (i != j && dist[i][j] <= distanceThreshold) {
                    ++num;
                }
            }

            if (num < min_num) {
                min_num = num;
                ans = i;
            }
        }
        
        return ans;
        
        
    }
};
```