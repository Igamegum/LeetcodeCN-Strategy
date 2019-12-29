
# Problem
[Link](https://leetcode-cn.com/problems/verbal-arithmetic-puzzle/)

# Solution

* 直接枚举所有字符可能的值，然后按题意模拟即可，主要不要使用非线性容器，[最朴素的做法](https://leetcode-cn.com/problems/verbal-arithmetic-puzzle/solution/shu-gei-stlxie-de-jiao-xun-by-igamegum/)
* 较优的做法是合并同类项，对于一个字母C，根据其所处的位置，预处理出其系数，比如字符串"CBDC",则字母C对整个字符串的贡献值值为C * 1000 + C * 1,所以其系数为 1001,这是一个合并同类项的过程
* 时间复杂度O(10! * k) K取决于算法常数

# Code
```cpp
class Solution {
public:

    
    //std::map<char, int> fac;
    //std::set<char> not_zero;
    bool not_zero[256];
    int fac[256];
    std::vector<char> chs;
    bool used[10];
        
    bool dfs(int id, int sum) {
        if (id >= chs.size()) {
            return sum == 0;
        }
        int st = 0;
        //if (not_zero.find(chs[id]) != not_zero.end()) st = 1;
        if (not_zero[ chs[id] ]) st = 1;
        for (int i = st; i < 10; ++i) {
            if (!used[i]) {
                used[i] = true;
                bool res = dfs(id + 1, sum + fac[chs[id]] * i);
                if (res)  return true;
                used[i] = false;
            }
        }
        return false;
    }
    
    bool isSolvable(vector<string>& words, string result) {
        //fac.clear();
        //not_zero.clear();
        memset(not_zero, 0, sizeof(not_zero));
        memset(fac, 0, sizeof(fac));
        chs.clear();
        std::set<char> S;
        memset(used, false, sizeof(used));
        
        
        for (int i = 0; i < words.size(); ++i) {
            int cur = 1;
            for (int j = words[i].size() - 1; j >= 0; --j) {
                fac[words[i][j]] += cur;
                cur *= 10;    
                S.insert(words[i][j]);
            }
            //if (words[i].size() > 0) not_zero.insert(words[i][0]);
            if (words[i].size() > 0) not_zero[ words[i][0] ] = true;
        }
        
        int cur = 1;
        for (int i = result.size() - 1; i >= 0; --i) {
            fac[result[i]] -= cur;
            cur *= 10;
            S.insert(result[i]);
            if (result.size() > 0) not_zero[ result[0] ] = true;
        }
        
        for (auto it = S.begin(); it != S.end(); ++it) chs.push_back(*it);
        
        bool ans = dfs(0, 0);
        
        return ans;
    }
};
```