# Problem
[Link](https://leetcode-cn.com/problems/min-cost-to-connect-all-points/)

# Solution
* 最小生成树
* 构造出所有的边，按照边的大小从小到大排序，以此获取能够使得集合数量减少的边，累加边的长度即可
* 时间复杂度：O(n*n*log(n^2))

# Code
```cpp
class Solution {
public:
    std::vector<int> bin;
    int find(int x) {
        return bin[x] == x ? x : bin[x] = find(bin[x]);
    }
    bool merge(int x, int y) {
        int fx = find(x);
        int fy = find(y);
        if (fx == fy) return false;
        bin[fx] = fy;
        return true;
    }
    int calc(std::pair<int, int> lhs, std::pair<int, int> rhs) {
        return std::abs(lhs.first - rhs.first) + std::abs(lhs.second - rhs.second);
    }
    void init(const int n) {
        bin = std::vector<int>(n, 0);
        for (int i = 0; i < n; ++i) {
            bin[i] = i;
        } 
    }
    struct Edge {
        int L;
        int R;
        int len;
        Edge(int l, int r, int ll) {
            L = l;
            R = r;
            len = ll;
        }
        const bool operator < (const Edge& T) const {
            return len < T.len;
        }
    };
    int minCostConnectPoints(vector<vector<int>>& points) {
        int n = points.size();
        std::vector<Edge> E;
        for (int i = 0; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {
                int len = calc(std::make_pair(points[i][0], points[i][1]), std::make_pair(points[j][0], points[j][1]));
                E.push_back( Edge(i, j, len) );
            }
        }
        std::sort(E.begin(), E.end());
        init(n);
        int cnt = 0;
        int ans = 0;
        for (int i = 0; i < E.size(); ++i) {
            if (cnt == n - 1) break;
            if (merge(E[i].L, E[i].R)) {
                ++cnt;
                ans += E[i].len;
            }
        }
        return ans;
    }
};
```