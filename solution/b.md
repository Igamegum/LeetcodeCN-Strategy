# Problem
[Link](https://leetcode-cn.com/problems/sequential-digits/)

# Solution

* 直接按位模拟即可


# Code
```cpp
class Solution {
public:
    int num_len(const int val) {
        std::stringstream ss;
        ss << val;
        return ss.str().size();
    }
    std::vector<int> func(const int len, const int min_val, const int max_val) {
        std::vector<int> ans;
        if (len > 9) return ans;
        for (int st = 1; st <= 9; ++st) {
            int val = 0;
            if (st + len - 1 > 9) break;
            for (int j = st; j < st + len; ++j) {
                val *= 10;
                val += j;
            }
            if (val > max_val) break;
            if (val >= min_val) ans.push_back(val);
        }
        return ans;
    }
    
    vector<int> sequentialDigits(int low, int high) {
        std::vector<int> ans;
        int len_l = num_len(low);
        int len_h = num_len(high);
        
        for (int i = len_l; i <= len_h; ++i) {
            std::vector<int> tmp = func(i, low, high);
            for (int j = 0; j < tmp.size(); ++j) {
                ans.push_back(tmp[j]);
            }
        }
        
        return ans;
    }
};
```