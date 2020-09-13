# Problem
[Link](https://leetcode-cn.com/problems/count-unhappy-friends/)

# Solution
* 直接模拟
* 时间复杂度：O(n*n*n)

# Code
```cpp
class Solution {
public:
    bool check(vector<vector<int>>& preferences, int aim, int a, int b) {
        int find = aim;
        for (int i = 0; i < preferences[aim].size(); ++i) {
            if (preferences[aim][i] == a || preferences[aim][i] == b) {
                find = preferences[aim][i];
                break;
            }
        }
        return find == a;
    }
    int unhappyFriends(int n, vector<vector<int>>& preferences, vector<vector<int>>& pairs) {
        int ans = 0;
        std::set<int> S;
        for (int i = 0; i < pairs.size(); ++i) {
            for (int j = 0; j < pairs.size(); ++j) {
                if (i == j) continue;
                
                do {
                    if (check(preferences, pairs[i][0], pairs[j][0], pairs[i][1]) && check(preferences, pairs[j][0], pairs[i][0], pairs[j][1])) {
                        S.insert(pairs[i][0]);
                        //break;
                    }
                    if (check(preferences, pairs[i][0], pairs[j][1], pairs[i][1]) && check(preferences, pairs[j][1], pairs[i][0], pairs[j][0])) {
                        S.insert(pairs[i][0]);
                        //break;
                    }
                    if (check(preferences, pairs[i][1], pairs[j][1], pairs[i][0]) && check(preferences, pairs[j][1], pairs[i][1], pairs[j][0])) {
                        S.insert(pairs[i][1]);
                        //break;
                    }
                    if (check(preferences, pairs[i][1], pairs[j][0], pairs[i][0]) && check(preferences, pairs[j][0], pairs[i][1], pairs[j][1])) {
                        S.insert(pairs[i][1]);
                        //break;
                    }
                } while (false);
            }
        }
        return S.size();
    }
};
```