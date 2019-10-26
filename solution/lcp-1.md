# Problem
[Link](https://leetcode-cn.com/problems/guess-numbers)

# Solution

直接遍历

# Code
```cpp
class Solution {
public:
    int game(vector<int>& guess, vector<int>& answer) {
        int ans = 0;
        for (int i = 0; i < std::min(guess.size(), answer.size()); ++i) {
            if (guess[i] == answer[i]) {
                ++ans;
            }
        }
        return ans;
    }
};
```