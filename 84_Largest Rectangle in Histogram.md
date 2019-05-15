>https://leetcode.com/problems/largest-rectangle-in-histogram/

**EXPRESSION**

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](https://assets.leetcode.com/uploads/2018/10/12/histogram.png)

Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].

![](https://assets.leetcode.com/uploads/2018/10/12/histogram_area.png)

The largest rectangle is shown in the shaded area, which has area = 10 unit.

**Example:**

    Input: [2,1,5,6,2,3]
    Output: 10

**COMPREHENSION**

*方法一*

遍历数组，每找到一个局部峰值，然后向前遍历所有的值，算出共同的矩形面积，每次保留最大值

```
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int res = 0;
	    for (int i = 0; i < heights.size(); ++i) {
		    if (i + 1 < heights.size() && heights[i] <= heights[i + 1])
		    	continue;
		    int minh = heights[i];
		    for (int j = i; j >= 0; --j) {
		    	minh = min(minh, heights[j]);
		    	res = max(res, minh*(i - j + 1));
		    }
	    }
	    return res;
    }
};
```

*方法二*

利用栈来解决，参考[boke](http://www.cnblogs.com/lichen782/p/leetcode_Largest_Rectangle_in_Histogram.html)

首先，如果栈是空的，那么索引i入栈。那么第一个i=0就进去吧。注意栈内保存的是索引，不是高度。然后i++。
![](https://images0.cnblogs.com/blog/466943/201307/17192556-87c3c19d702f4f7d80f9151e3abf3839.png)

然后继续，当i=1的时候，发现h[i]小于了栈内的元素，于是出栈。（由此可以想到，哦，看来stack里面只存放**单调递增的索引**）

这时候stack为空，所以面积的计算是h[t] * i.t是刚刚弹出的stack顶元素。也就是蓝色部分的面积。
![](https://images0.cnblogs.com/blog/466943/201307/17193427-72afd2effb414859b8a8357f2af576d7.png)

继续。这时候stack为空了，继续入栈。注意到只要是连续递增的序列，我们都要keep pushing，直到我们遇到了i=4，h[i]=2小于了栈顶的元素。
![](https://images0.cnblogs.com/blog/466943/201307/17194005-14511ed367484101a307e4c00c953048.png)

这时候开始计算矩形面积。首先弹出栈顶元素，t=3。即下图绿色部分。
![](https://images0.cnblogs.com/blog/466943/201307/17194440-81492510db734653a8ac3f334f1e58e7.png)

接下来注意到栈顶的（索引指向的）元素还是大于当前i指向的元素，于是出栈，并继续计算面积，桃红色部分。
![](https://images0.cnblogs.com/blog/466943/201307/17194943-e96e6e654b744b70bd35602691dae7d6.png)

最后，栈顶的（索引指向的）元素大于了当前i指向的元素，循环继续，入栈并推动i前进。直到我们再次遇到下降的元素，也就是我们最后人为添加的dummy元素0.
![](https://images0.cnblogs.com/blog/466943/201307/17195453-d757bf1ba1ac44d08f71e9ac1d87a654.png)

同理，我们计算栈内的面积。由于当前i是最小元素，所以所有的栈内元素都要被弹出并参与面积计算。
![](https://images0.cnblogs.com/blog/466943/201307/17195959-3aec6aaeb9534632a0350a045aedbf2b.png)

注意我们在计算面积的时候已经更新过了maxArea。

总结下，我们可以看到，stack中总是保持递增的元素的索引，然后当遇到较小的元素后，依次出栈并计算栈中bar能围成的面积，直到栈中元素小于当前元素。

```
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int res = 0;
	    stack<int> s;
	    heights.push_back(0);//dummy=0;
	    for (int i = 0; i < heights.size(); ++i) {
	    	while (!s.empty() && heights[s.top()] >= heights[i]) {
	    		int cur = s.top();
	    		s.pop();
	    		res = max(res, heights[cur] * (s.empty() ? i : (i - s.top() - 1)));
	    	}
	    	s.push(i);
	    }
	    return res;
    }
};
```
