# Problem
[Link](https://leetcode-cn.com/problems/sort-integers-by-the-power-value/)

# Solution

* 直接模拟即可
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    int weight( int x) {
        int ans = 0;
        while (x != 1) {
            if (x & 1) x = x * 3 + 1;
            else x >>= 1;
            ++ans;
        }
        return ans;
    }
    
    struct Node {
        int val;
        int wei;
        Node(int val, int wei) {
            this->val = val;
            this->wei = wei;
        }
        const bool operator < (const Node & T)const {
            if (wei != T.wei) return wei < T.wei;
            return val < T.val;
        }
    };
    
    int getKth(int lo, int hi, int k) {
        std::vector<Node> num;
        for (int i = lo; i <= hi; ++i) {
            int wei = weight(i);
            num.push_back(Node(i, wei));
        }
        std::sort(num.begin(), num.end());
        return num[k - 1].val;
    }
};
```