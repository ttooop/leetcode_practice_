>https://leetcode.com/problems/spiral-matrix/

**expression**

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

**Example 1:**

    Input:
    [
     [ 1, 2, 3 ],
     [ 4, 5, 6 ],
     [ 7, 8, 9 ]
    ]
    Output: [1,2,3,6,9,8,7,4,5]

Example 2:

    Input:
    [
      [1, 2, 3, 4],
      [5, 6, 7, 8],
      [9,10,11,12]
    ]
    Output: [1,2,3,4,8,12,11,10,9,5,6,7]
    
**comprehension**

要求将一个矩阵按照螺旋顺序打印出来，两种方法：：

*方法一* 坐标的转换

```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.empty()||matrix[0].empty())
            return {};
        vector<int> res;
        int m=matrix.size(),n=matrix[0].size();
        int c=m>n?(n+1)/2:(m+1)/2;
        int p=m,q=n;
        for(int i=0;i<c;++i,p-=2,q-=2){
            for(int col=i;col<i+q;++col)
                res.push_back(matrix[i][col]);
            for(int row=i+1;row<i+p;++row)
                res.push_back(matrix[row][i+q-1]);
            if(p==1||q==1)
                break;
            for(int col=i+q-2;col>=i;--col)
                res.push_back(matrix[i+p-1][col]);
            for(int row=i+p-2;row>i;--row)
                res.push_back(matrix[row][i]);
        }
        return res;
        
    }
};
```

*方法二* 用变量up,down,left,right来模拟螺旋过程

```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if (matrix.empty() || matrix[0].empty())
		    return {};
	    int m = matrix.size(), n = matrix[0].size();
	    vector<int> res;
	    int up = 0, down = m - 1, left = 0, right = n - 1;
	    while (true) {
		    for (int j = left; j <= right; ++j)
	    		res.push_back(matrix[up][j]);
	    	if (++up > down)
	    		break;
	    	for (int i = up; i <= down; ++i)
	    		res.push_back(matrix[i][right]);
	    	if (--right < left)
	    		break;
	    	for (int j = right; j >= left; --j)
	    		res.push_back(matrix[down][j]);
	    	if (--down < up)
	    		break;
	    	for (int i = down; i >= up; --i)
	    		res.push_back(matrix[i][left]);
	    	if (++left > right)
		    	break;
	    }
	    return res;
    }
};
```
