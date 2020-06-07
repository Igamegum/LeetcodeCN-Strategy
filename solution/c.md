# Problem
[Link]()

# Solution
* 考虑用vector或者list存储访问历史，用一个变量idx 表示当前正在访问的网页，变量siz表示可以forward到的最大下标。显然，visit操作会将siz重置为idx,其他只要注意边界判断即可
* 时间复杂度O(1)

# Code
```cpp
class BrowserHistory {
public:
    std::vector<std::string> his;
    int idx;
    int siz;
    BrowserHistory(string homepage) {
        his.clear();
        his.push_back(homepage);
        idx = 0;
        siz = 0;
    }
    
    void visit(string url) {
        if (his.size() == idx + 1) {
            his.push_back(url);
        } else {
            his[idx + 1] = url;
        }
        ++idx;
        siz = idx;
    }
    
    string back(int steps) {
        int bidx = std::max(0, idx - steps);
        idx = bidx;
        return his[idx];
    }
    
    string forward(int steps) {
        int fidx = std::min(siz, idx + steps);
        idx = fidx;
        return his[idx];
    }
};

```