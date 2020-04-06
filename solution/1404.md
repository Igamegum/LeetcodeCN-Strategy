# Problem
[Link](https://leetcode-cn.com/problems/number-of-steps-to-reduce-a-number-in-binary-representation-to-one/)

# Solution

* 直接模拟即可
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    string add(string s) {
        int index = s.size() - 1;
        int per = 1;
        int sum = 0;
        while (index >= 0) {
            sum = s[index] - '0' + per;
            s[index] = (sum % 2) +  '0';
            per = sum / 2;
            --index;
            if (!per) break;
        }
        if (per) return "1" + s;
        return s;
    }
    
    string div(string s) {
        int siz = s.size();
        return s.substr(0, siz - 1);
    }
    
    int calc(string s) {
        int ans = 0;
        while (s.size() > 1) {
            if (s[s.size() - 1] == '0') s = div(s);
            else s = add(s);
            ++ans;
        }   
        return ans;
    }
    
    int numSteps(string s) {
        return calc(s);
    }
};
```