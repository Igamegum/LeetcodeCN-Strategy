# Problem
[Link](https://leetcode-cn.com/problems/minimum-insertions-to-balance-a-parentheses-string/)

# Solution
* 直接模拟
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    int minInsertions(string s) {
        int n = s.size();
        int sum = 0;
        int ans = 0;
        for (int i = 0; i < n; ++i) {
            //std::cout << i << " " << sum << " " << ans << std::endl;
            if (sum < 0 && s[i] == '(') {
                sum = abs(sum);    
                if (sum & 1) ++sum, ++ans;
                ans += sum / 2;
                sum = 0;
            } else if (sum > 0 && sum & 1 && s[i] == '(') {
                ans += 1;
                sum -= 1;
            }
            sum += s[i] == '(' ? 2 : -1;
        }        
        
        if (sum > 0) ans += sum;
        else if (sum < 0) {
            sum = abs(sum);
            if (sum & 1) ++sum, ++ans;
            ans += sum / 2;
        }
        
        return ans;
    }
};
```