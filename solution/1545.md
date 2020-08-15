# Problem
[Link](https://leetcode-cn.com/problems/find-kth-bit-in-nth-binary-string/)

# Solution
* 直接计算K是上一层数字的第几位置
* 时间复杂度：O(n)

# Code
```cpp

    
                                        

class Solution {
public:
    
    const std::vector<int> len = {1,3,7,15,31,63,127,255,511,1023,2047,4095,8191,16383,32767,65535,131071,262143,524287,1048575};
    
    char findKthBit(int n, int k) {
        int cnt = 0;
        while (n) {
            if (n == 1) return cnt & 1 ? '1' : '0';
            if (k == len[n - 2] + 1) {
                return cnt & 1 ? '0' : '1';
            }
            if (k <= len[n - 2]) {
                --n;
            } else {
                k -= len[n - 2] + 1;
                k = len[n - 2] - k + 1;
                --n;
                ++cnt;
            }
            
        }
        return '0';
    }
};
```