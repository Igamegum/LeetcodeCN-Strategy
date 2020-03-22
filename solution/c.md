# Problem
[Link](https://leetcode-cn.com/problems/cinema-seat-allocation/)

# Solution

* 直接模拟即可
* 时间复杂度O(n * logn)

# Code
```cpp
class Solution {
public:

    int check(std::vector<int> arr) {
        if (arr[2] && arr[3] && arr[4] && arr[5] && arr[6] && arr[7] && arr[8] && arr[9]) return 2;
        if (arr[2] && arr[3] && arr[4] && arr[5]) return 1;
        if (arr[6] && arr[7] && arr[8] && arr[9]) return 1;
        if (arr[4] && arr[5] && arr[6] && arr[7]) return 1;
        return 0;
    }

    int maxNumberOfFamilies(int n, vector<vector<int>>& reservedSeats) {

        std::map<int, std::vector<int> > seat;
        for (int i = 0; i < reservedSeats.size(); ++i) {
            int r = reservedSeats[i][0];
            int c = reservedSeats[i][1];
            if (seat.find(r) != seat.end()) {
                seat[r][c] = 0;
            } else {
                seat[r] = std::vector<int>(11, 1);
                seat[r][c] = 0;
            }
        }
        
        int ans = 0;
        ans += ( n - seat.size() ) * 2;
        for (auto it = seat.begin(); it != seat.end(); ++it) {
            ans += check(it->second);
        }
        
        return ans;
    }
};
```