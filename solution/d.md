# Problem
[Link](https://leetcode-cn.com/problems/stone-game-v/)

# Solution
* 直接搜索即可，需要记忆化
* 时间复杂度：O(n*n*logn)

# Code
```cpp
int mp[510][510];
class Solution {
public:
    
    //std::map< std::pair<int, int>, int > mp;
    int dfs(int L, int R, vector<int>& V) {
        if (L >= R) return 0;
        std::pair<int, int> id = std::make_pair(L, R);
        //if (mp.find(id) != mp.end()) return mp[id];
        if (mp[L][R] != -1) return mp[L][R];
        
        int sum = 0;
        for (int i = L; i <= R; ++i) sum += V[i];
        int cur = 0;
        int best_ans = 0;
        int ans = 0;
        for (int i = L; i < R; ++i) {
            cur += V[i];
            if (cur < sum - cur) {
                best_ans = cur + dfs(L, i, V);
            } else if (cur > sum - cur) {
                best_ans = sum - cur +  dfs(i + 1, R, V);
            } else {
                int lhs = dfs(L, i, V);
                int rhs = dfs(i + 1, R, V);
                best_ans = cur + std::max(lhs, rhs);
            }
            ans = std::max(ans, best_ans);
        }
        //mp[id] = ans;
        //return mp[id];
        mp[L][R] = ans;
        return ans;
        
    }
    int stoneGameV(vector<int>& V) {
        //mp.clear();
        memset(mp, -1, sizeof(mp));
        return dfs(0, V.size() - 1, V);
    }
};
```