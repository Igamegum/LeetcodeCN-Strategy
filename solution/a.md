# Problem
[Link]()

# Solution
* 直接模拟
* 时间复杂度：O(n)

# Code
```cpp
class Solution {
public:
    std::string parse_day(std::string date) {
        int siz = date.size();
        std::string str = date.substr(0, siz - 2);
        if (str.size() < 2) str = std::string(1, '0') + str;
        return str;
    }
    
    //"Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"
    std::string parse_mon(std::string mon) {
        std::map<std::string, std::string> mp;
        mp["Jan"] = "01";
        mp["Feb"] = "02";
        mp["Mar"] = "03";
        mp["Apr"] = "04";
        mp["May"] = "05";
        mp["Jun"] = "06";
        mp["Jul"] = "07";
        mp["Aug"] = "08";
        mp["Sep"] = "09";
        mp["Oct"] = "10";
        mp["Nov"] = "11";
        mp["Dec"] = "12";
        return mp[mon];
    }
    
    std::string parse_year(std::string year) {
        return year;
    }
    
    string reformatDate(string date) {
        std::string day;
        std::string mon;
        std::string year;
        std::string str;
        int cnt = 0;
        for (int i = 0; i < date.size(); ++i) {
            if (date[i] == ' ' && cnt == 0) {
                ++cnt;
                day = parse_day(str);
                str = "";
            } else if (date[i] == ' ' && cnt == 1){
                mon = parse_mon(str);
                str = "";
            } else {
                str += std::string(1, date[i]);
            }
        }
        year = parse_year(str);
        
        std::string ans;
        ans = year + "-" + mon + "-" + day;
        return ans;
    }
};
```