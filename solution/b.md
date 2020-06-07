# Problem
[Link]()

# Solution
* 最小堆模拟，这道题内存卡的比较紧
* 时间复杂度O(n*logk)

# Code
```cpp
class Solution {
public:

    vector<int> getStrongest(vector<int>& arr, int k) {
 
        std::sort(arr.begin(), arr.end());
        int n = arr.size();
        int mid = arr[(n - 1) / 2];
           
        typedef std::pair<int, int> PII;
        std::priority_queue<PII, std::vector<PII>, std::greater<PII> > q;
        
        for (int i = 0; i < k; ++i) {
            PII p = std::make_pair(abs(arr[i] - mid), arr[i]);
            q.push(p);
        }
        
        for (int i = k; i < arr.size(); ++i) {
            PII p = std::make_pair(abs(arr[i] - mid), arr[i]);
            PII t = q.top();
            if (p.first > t.first || (p.first == t.first && p.second > t.second)) {
                q.pop();
                q.push(p);
            }
        }
        
        std::vector<int> ans;
        while (!q.empty()) {
            PII t = q.top();
            ans.push_back(t.second);
            q.pop();
        }
  
        return ans;
    }
};
```