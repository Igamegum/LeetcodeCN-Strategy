# Problem
[Link](https://leetcode-cn.com/problems/find-the-kth-smallest-sum-of-a-matrix-with-sorted-rows/)

# Solution

* 注意到k最多只有200，考虑一个比较暴力的解法
* 首选，第1小的数字，一定是所有行取第一个数字，记录下当前所选出的值对应的每一行选取的数字的下标，然后枚举每一行分别往后取一个数字，将得到的新的数字和放入到set中
* 如此操作K次，便能找到第K小的数字和
* 时间复杂度O(n * k * log(n * k))

# Code
```cpp
class Solution {
public:
    int kthSmallest(vector<vector<int>>& mat, int k) {

        int n = mat.size();
        int m = mat[0].size();
        std::set< std::pair<int, std::vector<int> > > S;
        int sum = 0;
        std::vector<int> id;
        for (int i = 0; i < n; ++i) {
            sum += mat[i][0];
            id.push_back(0);
        }
        S.insert(std::make_pair(sum, id));

        while (k > 1) {
            std::pair<int, std::vector<int> > a = *S.begin();
            S.erase(a);

            for (int i = 0; i < n; ++i) {
                if (a.second[i] + 1 < m) {
                    std::pair<int, std::vector<int> > b;
                    b.first = a.first + mat[i][ a.second[i] + 1 ] - mat[i][ a.second[i] ];
                    b.second = a.second;
                    b.second[i] += 1;
                    S.insert(b);
                }
            }
            --k;
        }

        return (*S.begin()).first;
    }
};
```