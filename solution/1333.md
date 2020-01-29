# Problem
[Link](https://leetcode-cn.com/problems/filter-restaurants-by-vegan-friendly-price-and-distance/)

# Solution

* 直接按题意模拟即可
* 时间复杂度O(n * logn)

# Code
```cpp
class Solution {
public:
    struct Node
    {
        int id;
        int ratings;
        Node(int idd, int ratingss)
        {
            id = idd;
            ratings = ratingss;
        }
        
        const bool operator < (const Node & T) const {
            if (ratings == T.ratings) return id > T.id;
            return ratings > T.ratings;
        }
    };
    
    vector<int> filterRestaurants(vector<vector<int>>& restaurants, int veganFriendly, int maxPrice, int maxDistance) {
        
        std::vector<Node> nodes;
        for (int i = 0; i < restaurants.size(); ++i) {
            if ((restaurants[i][2]  == 1 && veganFriendly == 1 ) || veganFriendly == 0) {
                if (restaurants[i][3] <= maxPrice && restaurants[i][4] <= maxDistance) {
                    Node node(restaurants[i][0], restaurants[i][1]);
                    nodes.push_back(node);
                }
            }
        }
        std::sort(nodes.begin(), nodes.end());
        std::vector<int> ans;
        for (int i = 0; i < nodes.size(); ++i) {
            ans.push_back(nodes[i].id);
        }
        return ans;
    }
};
```