# Problem
[Link](https://leetcode-cn.com/problems/design-a-stack-with-increment-operation/)

# Solution

* 直接模拟即可

# Code
```cpp
class CustomStack {
public:
    std::vector<int> vals;
    int num;
    int max_size;
    CustomStack(int maxSize) {
        num = 0;
        max_size = maxSize;
        //vals.clear();
        vals = std::vector<int>(maxSize, 0);
    }
    
    void push(int x) {
        if (num < max_size) {
            vals[num] = x;
            ++num;
        }
    }
    
    int pop() {
        if (num == 0) return -1;
        --num;
        return vals[num];
    }
    
    void increment(int k, int val) {
        int ed = std::min(k, num);
        for (int i = 0; i < ed; ++i) {
            vals[i] += val;
        }
    }
};
```