# Problem
[Link](https://leetcode-cn.com/problems/edit-distance/)

# Solution

* 首先，最后一定是落点某个点i，能够直接从点i往右跳跳出游戏机，那么这个问题就变成，维护点i到0号点的最短距离即可。
* 不妨设dis[i]代表从点0到点i的最短距离，用一个队列保存当前个到达的点，如果dis[i]未被更新，那么就更新dis[i]，并且将点i放入队列
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int minJump(vector<int>& jump) {
        int n = jump.size();
        std::vector<int> dis(n, -1);
        std::queue<int> q;
        dis[0] = 0;
        q.push(0);
        int last = 1;
        while (!q.empty()) {
            int id = q.front(); 
            q.pop();
            if (id + jump[id] >= n) {
                return dis[id] + 1;
            }
            int nx = id + jump[id];
            if (dis[nx] == -1) {
                dis[nx] = dis[id] + 1;
                q.push(nx);
            }

            while (last < id) {
                if (dis[last] != -1) {
                   // dis[last] = std::min(dis[last], dis[id] + 1);
                } else {
                    dis[last] = dis[id] + 1;
                    q.push(last);
                }
                ++last;
            }

        }
        return -1;
    }
};
```