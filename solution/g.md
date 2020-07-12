# Problem
[Link](https://leetcode-cn.com/problems/path-with-maximum-probability/)

# Solution
* BFS，优先搜索当前概率大的点
* 时间复杂度：O(m*n)

# Code
```cpp
class Solution {
public:
    struct Node {
        int pos;  
        double rate;
        Node(int p, double r) {
            pos = p;
            rate = r;
        }
        const bool operator < (const Node &T) const {
            return rate < T.rate;
        }
    };
    
    std::vector< std::vector<int> > E;
    std::vector<double>  vis;
    std::map<std::pair<int, int>, double> rates;
    
    double BFS(int st, int ed) {
        Node node(st, 1);
        vis[st] = 1.0;
        
        std::priority_queue<Node> q;
        q.push(node);
        while (!q.empty()) {
            node = q.top();
            q.pop();
            if (node.pos == ed) return node.rate;
            
            for (int i = 0; i < E[node.pos].size(); ++i) {
                int nx = E[node.pos][i];
                double rate = rates[std::make_pair(node.pos, nx)];
                double new_rate = rate * node.rate;
                if (new_rate > vis[nx]) {
                    vis[nx] = new_rate;
                    Node tmp(nx, rate * node.rate);    
                    q.push(tmp);
                }
            }
        }
        return 0.0;
    }
    
    double maxProbability(int n, vector<vector<int>>& edges, vector<double>& succProb, int start, int end) {
        E.resize(n);
        rates.clear();
        for (int i = 0; i < edges.size(); ++i) {
            int a = edges[i][0];
            int b = edges[i][1];
            E[a].push_back(b);
            E[b].push_back(a);
            rates[std::make_pair(a, b)] = succProb[i];
            rates[std::make_pair(b, a)] = succProb[i];
        }
        vis = std::vector<double>(n, 0.0);

        return BFS(start, end);
    }
};
```