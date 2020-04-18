# Problem
[Link](https://leetcode-cn.com/problems/html-entity-parser/)

# Solution

* 直接模拟，这题对时限貌似卡的比较紧，string的api都不能直接用了
* 时间复杂度O(n^2)

# Code
```cpp
class Solution {
public:
    string entityParser(string text) {
        std::map<string, string> mp;
        mp["&quot;"] = "\"";
        mp["&apos;"] = "'";
        mp["&amp;"] = "&";
        mp["&gt;"] = ">";
        mp["&lt;"] = "<";
        mp["&frasl;"] = "/";
        
        std::string ans;
        int id = 0;
        while (id < text.size()) {
            bool find = false;
            for (auto it = mp.begin(); it != mp.end(); ++it) {
                string fi = it->first;
                string se = it->second;
                //if (id + fi.size() <= text.size() && text.substr(id, fi.size()) == fi) {
                if (id + fi.size() <= text.size()) {
                    bool cmp = true;
                    for (int i = id; i < id + fi.size(); ++i) {
                        if (text[i] != fi[i - id]) {
                            cmp = false;
                            break;
                        }
                    }
                    
                    if (cmp) {
                        find = true;
                        ans += se;
                        id += fi.size();
                        break;    
                    }
                    
                }
            }    
            
            if (!find) {
                ans += text[id];
                ++id;
            }
        }
        
        
        return ans;
    }
};
```