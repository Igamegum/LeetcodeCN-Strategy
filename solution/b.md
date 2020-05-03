# Problem
[Link](https://leetcode-cn.com/problems/max-difference-you-can-get-from-changing-an-integer/)

# Solution

* 直接模拟即可
* 时间复杂度O(n*9*9)

# Code
```cpp
class Solution {
public:
    bool parse(const std::string ans, int x, int y, int &diff) {
        if (x == y) return false;
        std::string temp = ans;
        for (int i = 0; i < temp.size(); ++i) {
            if (temp[i] - '0' == x) {
                temp[i] = '0' + y;
            }
        }
        
        std::stringstream bb(temp);
    
        int b;    
        bb >> b;
        int c = pow(10.0, ans.size() - 1);
        if (b == 0) return false;
        if (b < c) return false;
        diff = b;
        return true;
    }
    
    int maxDiff(int num) {

        
        std::stringstream ss;
        ss << num;
        std::vector<int> sq;
        for (int i = 0; i <= 9; ++i) {
            for (int y = 0; y <= 9; ++y) {
                int val = 0;
                bool res = parse(ss.str(), i, y, val);
                if (res) {
                    sq.push_back(val);
                }
            }
        } 
        
        std::sort(sq.begin(), sq.end());
        int n = sq.size();
        if (n <= 1) return 0;
        
        return sq[n - 1] - sq[0];
    }
};
```