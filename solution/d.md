# Problem
[Link](https://leetcode-cn.com/problems/jump-game-v/)

# Solution

* 显然，arr小的不能跳到arr大的，arr大的可以跳到arr小的，相当于arr大的依赖于arr小的，所以必须要先求出arr小的答案。对于arr[i],相当于在其可跳跃的范围内取最大值+1即可。
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    int maxJumps(vector<int>& arr, int d) {
        std::vector< std::pair<int,int> > vec;
        std::vector<int> best(arr.size(), 1);
        for (int i = 0; i < arr.size(); ++i) {
            vec.push_back(std::make_pair(arr[i], i));
        }

        std::sort(vec.begin(), vec.end());
        int ans = 1;
        for (int i = 0; i < vec.size(); ++i) {
            int st = vec[i].second;
            
            int id = st;
            while (id - 1 >= 0 && arr[id - 1] < arr[st] && st - id + 1 <= d) {
                best[st] = std::max(best[st], best[id - 1] + 1);
                id = id - 1;
            }

            id = st;
            while (id + 1 < arr.size() && arr[id + 1] < arr[st] && id + 1 - st <= d) {
                best[st] = std::max(best[st], best[id + 1] + 1);
                id = id + 1;
            }
            ans = std::max(ans, best[st]);
        }

        return ans;
    }
};
```