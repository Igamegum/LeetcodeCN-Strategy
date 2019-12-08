# Problem
[Link](https://leetcode-cn.com/problems/minimum-number-of-flips-to-convert-binary-matrix-to-zero-matrix/)

# Solution

* 由于数据范围很小，mat只有3*3， 而每个元素只有0和1两种状态，所以总的状态数不超过2^9，直接爆搜即可
* 时间复杂度O(2^9 * 9)

# Code
```cpp
class Solution {
public:
    int m;
    int n;
    std::set<int> S;
    
    bool check(const std::vector<std::vector<int>> & mat) {
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (mat[i][j] != 0) return false;
            }
        }
        return true;
    }
    
    int hash_code(const std::vector<std::vector<int>> & mat) {
        int sum = 0;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                sum *= 10;
                sum += mat[i][j];
            }
        }
        return sum;
    }
    std::vector< std::vector<int> > flip(const std::vector<std::vector<int>> & mat, int x, int y) {
        std::vector< std::vector<int> > ans(mat);
        ans[x][y] = 1 - ans[x][y];
        if (x - 1 >= 0) ans[x - 1][y]  = 1 - ans[x - 1][y];
        if (x + 1 < m)  ans[x + 1][y]  = 1 - ans[x + 1][y];
        if (y - 1 >= 0) ans[x][y - 1]  = 1 - ans[x][y - 1];
        if (y + 1 < n)  ans[x][y + 1]  = 1 - ans[x][y + 1];
        return ans;
    }
    struct Node {
        int step;
        std::vector< std::vector<int> > mat;
    };
    
    int BFS(const vector<vector<int>>& mat) {
        std::queue<Node> q;
        Node node;
        node.mat = mat;
        node.step = 0;
        q.push(node);
        S.insert(hash_code(mat));
        
        while (!q.empty()) {
            node = q.front();
            q.pop();
            if (check(node.mat)) return node.step;
            for (int i = 0; i < m; ++i) {
                for (int j = 0; j < n; ++j) {
                    Node tmp;
                    tmp.mat = flip(node.mat, i, j);
                    tmp.step = node.step + 1;
                    int code = hash_code(tmp.mat);
                    if (S.find(code) == S.end()) {
                        S.insert(code);
                        q.push(tmp);
                    }
                }
            }
        }
        return -1;
    }
    
    int minFlips(vector<vector<int>>& mat) {
        m = mat.size();
        n = mat[0].size();
        S.clear();
        return BFS(mat);
        
    }
};
```