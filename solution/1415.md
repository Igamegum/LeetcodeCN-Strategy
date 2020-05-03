# Problem
[Link](https://leetcode-cn.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/)

# Solution

* 这题可以采用计数的方式完成，首先第一位有a,b,c这三种选择，往后的每一位只有两种选择，也就是说，如果第i位确定了，那么后面所有的组合数就是确定的，那么只需要根据k的值，判定答案会落在那个组合即可
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    
    
    string getHappyString(int n, int k) {
        std::string ans;
        int base = 1 << (n - 1);
        int total = 3 * base;
        
        if (total < k) return ans;
        
        if (base >= k) {
            ans += "a";
        } else if (base * 2 >= k) {
            ans += "b";
            k -= base;
        } else {
            ans += "c";
            k -= base;
            k -= base;
        }
        
        while (k && ans.size() < n) {
			int siz = ans.size();
			int base = 1 << (n - siz - 1);
			if (base >= k) {
				if (ans[siz - 1] == 'a') ans += "b";
				else if (ans[siz - 1] == 'b') ans += "a";
				else ans += "a";
			}
			else {
				if (ans[siz - 1] == 'a') ans += "c";
				else if (ans[siz - 1] == 'b') ans += "c";
				else ans += "b";
				k -= base;
			}
        }
        
        return ans;
    }
};
```