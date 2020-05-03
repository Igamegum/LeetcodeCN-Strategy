# Problem
[Link](https://leetcode-cn.com/problems/na-ying-bi/)

# Solution

* 对于字符ch，只需要判断当前在叫的青蛙中，有没有某个青蛙下一个要叫的字符是ch。考虑维护当前青蛙最后一个叫的字符，那么只需要将找到的青蛙的最后一个叫的字符替换成ch即可
* 假定当前青蛙叫的最后一个字符是ch，分别对ch维护一个set，set里面存储的是青蛙的编号
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    int minNumberOfFrogs(string croakOfFrogs) {

        std::map<char, char> mp;
        mp['c'] = 'k';
        mp['r'] = 'c';
        mp['o'] = 'r';
        mp['a'] = 'o';
        mp['k'] = 'a';
        
        
        std::map<char, std::set<int>> pos;
        pos['c'] = std::set<int>();
        pos['r'] = std::set<int>();
        pos['o'] = std::set<int>();
        pos['a'] = std::set<int>();
        pos['k'] = std::set<int>();
        
        int cnt = 0;
        
        for (int i = 0; i < croakOfFrogs.size(); ++i) {
            char ch = croakOfFrogs[i];
            bool find = false;
            char aim = mp[ch];
            
            if (pos[aim].size() > 0) {
                find = true;
                int id = *(pos[aim].begin());
                pos[aim].erase(id);
                pos[ch].insert(id);
            } 
            
            if (!find) {
                if (ch != 'c') return -1;
                ++cnt;
                pos['c'].insert(cnt);
            }
        }
        
        for (auto it = pos.begin(); it != pos.end(); ++it) {
            char ch = it->first;
            if (ch != 'k' && pos[ch].size() > 0) return -1;
        }
        
        return cnt;

        
    }
};
```