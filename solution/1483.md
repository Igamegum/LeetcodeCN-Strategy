# Problem
[Link](https://leetcode-cn.com/problems/kth-ancestor-of-a-tree-node/)

# Solution
* 数据范围小，直接暴力的O(n^2)可解
* 查询时间复杂度O(k / sqrt(n))，构造时间复杂度O(n)

# Code
```cpp
class TreeAncestor {
public:

    std::vector< std::vector<int> > edge;
    std::vector<int> fa;
    int Root;
    
    int Base = 100;
    std::vector<int> UP;
    std::vector<int> ups;

    
    void dfs(int root, int dep) {
        
        
        if (dep >= Base) {
            UP[root] = ups[dep - Base];
        }
        
        ups[dep] = root;
        
        for (int i = 0; i < edge[root].size(); ++i) {
            dfs(edge[root][i], dep + 1);
        }
    }

    
    int find(int root, int k) {
        int ans = root;

        while (UP[ans] != -1 && k >= Base) {
            ans = UP[ans];
            k -= Base;
        }
        for (int i = 1; i <= k; ++i) {
            if (ans == -1) return ans;
            ans = fa[ans];
        }
        return ans;
    }
    

    
    TreeAncestor(int n, vector<int>& parent) {
        
        Base = sqrt(n);
       
        UP   = std::vector<int>(n, -1);
        ups  = std::vector<int>(n, -1);
       
        edge = vector< std::vector<int> >(n, vector<int>(0));
        fa = parent;
        
        for (int i = 0; i < parent.size(); ++i) {
            if (parent[i] == -1) {
                Root = i;
            } else {
                edge[parent[i]].push_back(i);
            }
        }
        
        dfs(Root, 0);
       
    }
    
    
    
    int getKthAncestor(int node, int k) {
        return find(node, k);
    }
};

/**
 * Your TreeAncestor object will be instantiated and called as such:
 * TreeAncestor* obj = new TreeAncestor(n, parent);
 * int param_1 = obj->getKthAncestor(node,k);
 */
```