# Problem
[Link](https://leetcode-cn.com/problems/search-suggestions-system/)

# Solution

* 首先将 products 排序，然后分别算出每个 product 和 searchWord 最长匹配前缀的长度
* 对于长度为 i 的searchWord的前缀，遍历 product 数组，匹配长度不小于 i 的单词都是符合答案的
* 时间复杂度O(products.length * searchWord.length)

# Code
```cpp
class Solution {
public:
    int same(const std::string& lhs, const std::string& rhs) {
        int len = std::min(lhs.size(), rhs.size());
        int ans = 0;
        for (int i = 0; i < len; ++i) {
            if (lhs[i] != rhs[i]) return ans;
            ++ans;
        }
        return ans;
    }
    
    vector<vector<string>> suggestedProducts(vector<string>& products, string searchWord) {
        std::sort(products.begin(), products.end());
        std::vector<int> prefix(products.size(), 0);
        for (int i = 0; i < products.size(); ++i) {
            prefix[i] = same(products[i], searchWord);
        }
        
        std::vector< std::vector<std::string> > ans;
        for (int i = 0; i < searchWord.length(); ++i) {
            std::vector<std::string> tmp;
            int max_same = 0;
            for (int j = 0; j < products.size(); ++j) {
                if (prefix[j] < i + 1) continue;
                tmp.push_back(products[j]);
            }
            
            std::vector<std::string> res(tmp.begin(), tmp.begin() + std::min(3, (int)tmp.size()));
            ans.push_back(res);
        }
        
        return ans;
    }
};
```