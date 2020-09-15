# Problem
[Link](https://leetcode-cn.com/problems/check-if-string-is-transformable-with-substring-sort-operations/)

# Solution
* 这题有很多种做法，这里介绍一下比赛时我的做法
* 对串t，依次分解成多个单调不下降的子串，比如串"34852"就会被分解为"348","5","2"这三个子串；这里代表的是，依次让区间相同的串s对应的子串变成与t相同的子串
* 假定t对应的子串的区间是[ml,mr]，那么就需要从s中寻找能变换成对应子串的区间[ml,sr]（能变换的标准是t对应的每种数字出现的次数，在s中出现的次数都不小于t）
* 不难发现，sr一定是大于等于mr的，对于sr大于mr的情况，说明[ml,sr]中存在[ml,mr]中不需要的字符，那么就需要通过排序交换出去，举个例子
* t[0,2] = "348", s[0,3] = "8453"，s子串中的这个'5'就是t中不需要的，假定第一个不需要的字符出现的下标为k，那么我们就需要对s[k,sr]作一次排序，目的是将不需要的字符交换出去（虽然不一定能全部交换出去）
* 接着对s的目标区间[ml, mr]作一次排序，最后再判断排序后的区间[ml,mr]，s和t是否完全匹配即可
* 时间复杂度：O(n*logn)

# Code
```cpp
class Solution {
public:
	bool cover(const std::vector<int>& shs, const std::vector<int>& ths) {
		for (int i = 0; i < shs.size(); ++i) {
			if (shs[i] < ths[i]) return false;
		}
		return true;
	}

	bool isTransformable(string s, string t) {
		std::vector<int> ths;
		std::vector<int> shs;
		int ml = 0;
		while (ml < t.size()) {
			int mr = ml;
			while (mr + 1 < t.size() && t[mr + 1] >= t[mr]) ++mr;

			ths = std::vector<int>(10, 0);
			shs = std::vector<int>(10, 0);
			for (int i = ml; i <= mr; ++i) ++ths[t[i] - '0'];
			int sr = ml;
			++shs[s[sr] - '0'];
			while (cover(shs, ths) == false && sr + 1 < s.size()) {
				++sr;
				++shs[s[sr] - '0'];
			}
			if (cover(shs, ths) == false) return false;
			int st = ml;
			std::vector<int> tmp(10, 0);
			for (int i = ml; i <= sr; ++i) {
				int val = s[i] - '0';
				++tmp[val];
				if (tmp[val] > ths[val]) {
					st = i;
					break;
				}
			}
			std::sort(s.begin() + st, s.begin() + sr + 1);
			std::sort(s.begin() + ml, s.begin() + mr + 1);
			for (int i = ml; i <= mr; ++i) {
				if (s[i] != t[i]) return false;
			}
			ml = mr + 1;
		}

		return true;
	}
};
```
