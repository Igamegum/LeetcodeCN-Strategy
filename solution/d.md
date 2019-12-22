# Problem
[Link](https://leetcode-cn.com/problems/maximum-candies-you-can-get-from-boxes/)

# Solution

* 对一个能获取到糖果的盒子，当且仅当这个盒子被拿出来，而且这个盒子是打开状态。对于一个能获取到糖果的盒子，能做的事情有三件，一是获取糖果，二是获取钥匙，三是取出其中的盒子。
* 对于能获取到糖果的盒子，将其放入到队列中，不断模拟打开盒子的过程即可。
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    bool open[1010];
    int has[1010];//是否已经获得该盒子
    bool get[1010];//是否拿过糖果了
    
    int maxCandies(vector<int>& status, vector<int>& candies, const vector<vector<int>>& keys, vector<vector<int>>& containedBoxes, vector<int>& initialBoxes) {
        
        
        memset(open, false, sizeof(open));
        memset(has, false, sizeof(has));
        memset(get, false, sizeof(get));
    
        for (int i = 0; i < status.size(); ++i) {
            open[i] = status[i] == 1 ? true : false;
        }    
        
        
        int ans = 0;
        std::queue<int> q;
        for (int i = 0; i < initialBoxes.size(); ++i) {
            has[initialBoxes[i]] = true;
            if (open[initialBoxes[i]]) {
                q.push(initialBoxes[i]);
            }
        }
        
        while (!q.empty()) {
            int node = q.front();
            q.pop();
            
            if (get[node] == false) {
                get[node] = true;
                
                ans += candies[node];
                
                for (int i = 0; i < containedBoxes[node].size(); ++i) {
                    int val = containedBoxes[node][i];
                    has[val] = true;
                    if (open[val] == true && !get[val]) {
                        q.push(val);
                    } 
                }
                
                for (int i = 0; i < keys[node].size(); ++i) {
                    int val = keys[node][i];
                    open[val] = true;
                    if (open[val] == true && has[val] && !get[val]) {
                        q.push(val);
                    } 
                }
            }        
            
        }
        
        return ans;
    }
    
};
```