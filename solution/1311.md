
# Problem
[Link](https://leetcode-cn.com/problems/get-watched-videos-by-your-friends/)

# Solution

* BFS，直接从出发点遍历图即可
* 注意不能使用DFS，假定存在点 a, b, c;存在路径[a, b], [b, c], [a, c];即 a,b,c 三点之间两两可以直接相达。假定所求的是从点a出发，距离为2的点，如果使用的是DFS，从点a出发后，先搜索到点b，继而搜索到点c，点c会判定为距离点
a为2的点，实际上点c距离点a为1。
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
 
    bool vis[110];
    std::map<std::string, int> mp;
    
     struct video{
        int cnt;
        std::string name;
        bool const operator < (const video& T) const {
            if (cnt == T.cnt) return name < T.name;
            return cnt < T.cnt;
        }
    };
    
    struct QNode {
      int id;
      int step;
    };
    
    void BFS(vector<vector<string>>& watchedVideos, vector<vector<int>>& friends, int id, int level)
    {
        queue<QNode> q;
        QNode node;
        node.id = id;
        node.step = 0;
        vis[id] = true;
        q.push(node);
        while (!q.empty()) {
            node = q.front();
            q.pop();
            if (node.step == level) {
                
                for (int i = 0; i < watchedVideos[node.id].size(); ++i) {
                    mp[ watchedVideos[node.id][i] ]++;
                }
                continue;
            }
            
            int nid = node.id;
            for (int i = 0; i < friends[nid].size(); ++i) {
                QNode temp;
                temp.id = friends[nid][i];
                temp.step = node.step + 1;
                if (vis[temp.id] == false) {
                    vis[temp.id] = true;
                    q.push(temp);
                }
            }
        }
        return;
    }

    
    vector<string> watchedVideosByFriends(vector<vector<string>>& watchedVideos, vector<vector<int>>& friends, int id, int level) {
    
        memset(vis, false ,sizeof(vis));
        mp.clear();
 
        vis[id] = true;
       
        BFS(watchedVideos, friends, id, level);
        
        std::vector<video> as;
        for (auto it = mp.begin(); it != mp.end(); ++it) {
            video vi;
            vi.name = it->first;
            vi.cnt = it->second;
            as.push_back(vi);
        }
        
        std::sort(as.begin(), as.end());
        
        std::vector<std::string> ans;
        for (int i = 0; i < as.size(); ++i) {
            ans.push_back(as[i].name);
        }
        return ans;
        
    }
};
```