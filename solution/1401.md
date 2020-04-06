# Problem
[Link](https://leetcode-cn.com/problems/circle-and-rectangle-overlapping/)

# Solution

* 判断圆与矩形相交，首先判断圆心是否在矩形内，其次判断圆心到 4 条线段的距离是否大于圆的半径
* 时间复杂度O(1)

# Code
```cpp
class Solution {
public:

	double PointToSegDist(double x, double y, double x1, double y1, double x2, double y2)
	{
		double cross = (x2 - x1) * (x - x1) + (y2 - y1) * (y - y1); 
		if (cross <= 0) return sqrt((x - x1) * (x - x1) + (y - y1) * (y - y1)); 

		double d2 = (x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1); 
		if (cross >= d2) return sqrt((x - x2) * (x - x2) + (y - y2) * (y - y2)); 

		double r = cross / d2;  
		double px = x1 + (x2 - x1) * r;
		double py = y1 + (y2 - y1) * r;
		return sqrt((x - px) * (x - px) + (py - y) * (py - y));

	}

	bool checkOverlap(int radius, int x_center, int y_center, int x1, int y1, int x2, int y2) {
		
		if (x_center >= std::min(x1, x2) && x_center <= std::max(x1, x2) && y_center >= std::min(y1, y2) && y_center <= std::max(y1, y2)) return true;

		if (radius >= PointToSegDist(x_center, y_center, x1, y1, x2, y1) ) return true;
		if (radius >= PointToSegDist(x_center, y_center, x1, y1, x1, y2)) return true;
		if (radius >= PointToSegDist(x_center, y_center, x2, y2, x1, y2)) return true;
		if (radius >= PointToSegDist(x_center, y_center, x2, y2, x2, y1)) return true;

		return false;
	}
};
``