# Problem
[Link](https://leetcode-cn.com/problems/group-the-people-given-the-group-size-they-belong-to/)

# Solution

* 假定一个用户所在的集合大小为G，那么groupSizes中一定至少有G个G（G的出现次数一定是G的倍数），假定G的出现次数为K*G，说明有K个group，它们的集合大小都为G。那么我们只要按照集合大小对用户进行分类，对于集合大小都为G的用户，只要G个一组构造答案即可。
* 时间复杂度O(n * n)

# Code
```cpp
class Solution {
public:
    vector<vector<int>> groupThePeople(vector<int>& groupSizes) {
        std::vector< std::vector<int> > mp;

        for (int i = 0; i < 510; ++i) {
            std::vector<int> tmp;
            mp.push_back(tmp);
        }
        
        for (int i = 0; i < groupSizes.size(); ++i) {
            int val = groupSizes[i];
            mp[val].push_back(i);
        }
        
        std::vector<std::vector<int>> ans;
        for (int i = 1; i < 510; ++i) {
            if (mp[i].size() > 0) {
                for (int j = 0; j < mp[i].size(); j += i) {
                    std::vector<int> tmp;
                    for (int k = j; k < j + i; ++k) {
                        tmp.push_back(mp[i][k]);
                    }
                    ans.push_back(tmp);
                }
            }
        }
        return ans;
    }
};
```