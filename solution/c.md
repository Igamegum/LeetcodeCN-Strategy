# Problem
[Link](https://leetcode-cn.com/problems/design-underground-system/)

# Solution

* 直接map模拟即可,(这里的数据里面一个人不会有两趟旅程)
* 时间复杂度O(nlogn * n)

# Code
```cpp
class UndergroundSystem {
public:
    std::map<int, std::pair<std::string, int>> in;
    //std::map<int, std::pair<std::string, int>> out;
    std::map<std::string, std::vector<int> > tour;
    UndergroundSystem() {
        in.clear();
        //out.clear();
        tour.clear();
    }
    
    void checkIn(int id, string stationName, int t) {
        in[id] = std::make_pair(stationName, t);
    }
    
    void checkOut(int id, string stationName, int t) {
        if (in.find(id) == in.end()) return;
        
        string in_name = in[id].first;
        int in_time = in[id].second;
        
        string tour_name = in_name + stationName;
        tour[tour_name].push_back(t - in_time);
    }
    
    double getAverageTime(string startStation, string endStation) {
        string tour_name = startStation + endStation;
        if (tour.find(tour_name) == tour.end()) return 0.0;
        double sum = 0.0;
        for (int i = 0; i < tour[tour_name].size(); ++i) {
            sum += tour[tour_name][i];
        }
        
        double ans = sum / tour[tour_name].size();
        return ans;
    }
};
```