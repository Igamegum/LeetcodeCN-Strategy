# Problem
[Link](https://leetcode-cn.com/problems/rank-teams-by-votes/)

# Solution

* 直接模拟即可

# Code
```cpp
class Solution {
public:
    struct Node {
        int vote[26];
		
		char ch;
        bool valid;
        
        void init(char chh) {
            ch = chh;
            valid = false;
            memset(vote, 0, sizeof(vote));
        }

        const bool operator < (const Node& T) const {
            for (int i = 0; i < 26; ++i) {
                if (vote[i] != T.vote[i]) {
                    return vote[i] < T.vote[i];
                }
            }
            return ch > T.ch;
        }

    };
	

    string rankTeams(vector<string>& votes) {
        
        std::vector<Node> node(26);
        for (int i = 0; i < 26; ++i) {
            node[i].init('A' + i);
        }
        
        for (int i = 0; i < votes.size(); ++i) {
            for (int j = 0; j < votes[i].size(); ++j) {
                char ch = votes[i][j];
                int id = ch - 'A';
                node[id].vote[j] += 1;
                node[id].valid = true;
            }
        }
        
        std::sort(node.begin(), node.end());
        
        std::string ans;
        for (int i = node.size() - 1; i >= 0; --i) {
            if (node[i].valid == true) {
                ans += node[i].ch;
            }
        }
        return ans;
    }
};

```