# Problem
[Link](https://leetcode-cn.com/problems/number-of-burgers-with-no-waste-of-ingredients/)

# Solution
* 直接推一下公式就行了
* 假定巨汉堡的总数为 a,那么就有 4 * a + 2 * (cheeseSlices - a) = tomatoSlices,化简得(a + cheeseSlices) = tomatoSlices / 2,判断一下非法情况就行

# Code
```cpp
class Solution {
public:
    vector<int> numOfBurgers(int tomatoSlices, int cheeseSlices) {
        std::vector<int> ans;
        if (tomatoSlices & 1) return ans;

        tomatoSlices = tomatoSlices / 2;
        int a = tomatoSlices - cheeseSlices;
        int b = cheeseSlices - a;
        if (a < 0 || b < 0) return ans;
        
        ans.push_back(a);
        ans.push_back(b);
        return ans;
    }
};
```