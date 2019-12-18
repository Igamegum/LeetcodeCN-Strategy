# Problem
[Link](https://leetcode-cn.com/problems/convert-binary-number-in-a-linked-list-to-integer/)

# Solution

* 直接模拟
* 时间复杂度O(n)

# Code
```cpp
class Solution {
public:
    int getDecimalValue(ListNode* head) {
        long long ans = 0;
        while (head) {
            ans <<= 1;
            ans += head->val;
            head = head->next;
        }
        return ans;
    }
};
```