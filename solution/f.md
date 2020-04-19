# Problem
[Link](https://leetcode-cn.com/problems/display-table-of-food-orders-in-a-restaurant/)

# Solution

* 利用map，维护餐桌号+食物对应的份数即可
* 时间复杂度O(nlogn)

# Code
```cpp
class Solution {
public:
    std::string int2str(const int val) {
        std::stringstream ss;
        ss << val;
        return ss.str();
    }
    int str2int(const std::string str) {
        stringstream ss;
        ss << str;
        int val;
        ss >> val;
        return val;
    }
    vector<vector<string>> displayTable(vector<vector<string>>& orders) {
        std::set<int> no;
        std::set<string> food;
        std::map<string, int> order;
        
        for (int i = 0; i < orders.size(); ++i) {
            no.insert( str2int(orders[i][1]) );
            food.insert(orders[i][2]);
            std::string temp = orders[i][1] + orders[i][2];
            order[temp]++;
        }
        
        std::vector< std::vector<string> > ans;
        std::vector<string> title;
        title.push_back("Table");
        for (auto it = food.begin(); it != food.end(); ++it) {
            title.push_back(*it);
        }
        
        ans.push_back(title);
        
        for (auto it = no.begin(); it != no.end(); ++it) {
            std::vector<string> sub;
            string num = int2str(*it);
            sub.push_back(num);
            for (auto fd : food) {
                string temp = num + fd;
                if (order.find(temp) != order.end()) {
                    sub.push_back( int2str(order[temp]) );
                } else {
                    sub.push_back("0");
                }
            }
            ans.push_back(sub);
        }
        
        return ans;
    }
};
```