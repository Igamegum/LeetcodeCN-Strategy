# Problem
[Link](https://leetcode-cn.com/problems/find-latest-group-of-size-m/)

# Solution
* 树状数组维护区间和，由于是求最后一个步骤，所以可以考虑直接倒着做，由添加1变为删除1
* 时间复杂度：O(nlogn)

# Code
```cpp
class Solution {
public:
    std::vector<int> tree;
    int lowbit(int x) {
        return x & -x;
    }
    void modify(int x, int n, int val) {
        while (x <= n ) {
            tree[x] += val;
            x += lowbit(x);
        }
    }
    int query(int x) {
        int sum = 0;
        while (x > 0) {
            sum += tree[x];
            x -= lowbit(x);
        }
        return sum;
    }
    
    int range(int L, int R) {
        int lhs = query(L - 1);
        int rhs = query(R);
        return rhs - lhs;
    }
    
    int findLatestStep(vector<int>& arr, int m) {
        int n = arr.size();
        tree = std::vector<int> (n + 1, 0);
        std::vector<int> dp(n + 1, 1);
        dp[0] = 0;
        int ans = -1;
        if (m == n) return n;
        for (int i = 0; i < arr.size(); ++i) {
            modify(arr[i], n, 1);
        }
        for (int i = arr.size() - 1; i >= 1; --i) {
            modify(arr[i], n, -1);
            dp[arr[i]] = 0;
            int L = arr[i] - m;
            if (L > 0 ) {
                int lsum = range(L, arr[i] - 1);
                if (lsum == m && dp[L - 1] == 0) {
                    //ans = std::max(ans, i + 1);
                    return i;
                }
                
            }
            
            int R = arr[i] + m;
            if (R <= n) {
                int rsum = range(arr[i] + 1, R);
                if (rsum == m && (R == n || dp[R + 1] == 0)){
                    //ans = std::max(ans, i + 1);
                    return i;
                }
                
            }
        }
        
        return ans;
    }   
};
```