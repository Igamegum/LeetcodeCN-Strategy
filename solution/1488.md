# Problem
[Link]()

# Solution
* 用一个map记录某个湖当前状态为灌满的天数，用一个set记录可以抽干湖泊的日子。如果某个湖泊当前是会下雨，并且之前是满的，就需要找一个在灌满天数之后能抽干湖泊的日子去抽干，否则无解。
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    vector<int> avoidFlood(vector<int>& rains) {
        int n = rains.size();
        
        std::set<int> zero;
        std::vector<int> ans(n, -1);
        std::vector<int> empty;
        std::map<int, int> full;
        bool can = true;
        
        for (int i = 0; i < rains.size(); ++i) {
            if (rains[i] > 0) {
                if (full.find(rains[i]) != full.end()) {
                    int d = full[rains[i]];
                    auto it = zero.lower_bound(d);
                    if (it == zero.end()) {
                        can = false;
                        break;
                    }
                    ans[*it] = rains[i];
                    zero.erase(it);
                }
                    
                full[rains[i]] =  i;

            } else {
                zero.insert(i);
            }
        }
        
        for (int i = 0; i < n; ++i) {
            if (rains[i] == 0 && ans[i] == -1) {
                ans[i] = 1;
            } 
        }
        
        return can ? ans : empty;
        
    }
};
```