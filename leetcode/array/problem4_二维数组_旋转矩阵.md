# 旋转矩阵

​		给你一幅由 `N × N` 矩阵表示的图像，其中每个像素的大小为 4 字节。请你设计一种算法，将图像旋转 90 度。不占用额外内存空间能否做到？

​		https://leetcode.cn/leetbook/read/array-and-string/clpgd/

```c++
// 思路：首先要推导出matrix[i][j]旋转90°会存放在matrix[j][n-i-1]
// 然后就是要确定需要遍历哪些元素
// 行从0遍历到n/2-1，列从row遍历到n-2-row

class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {

        int n = matrix.size();
        // 旋转：row,col -> col,N-row-1
        for (int row = 0; row <= n/2-1; row++)// 行从0遍历到n/2-1
        {
			for (int col = row; col <= n-2-row; col++)// 列从row遍历到n-2-row
            {
            	int i = row, j = col;// i,j存储要旋转的行列
                int num = matrix[i][j];// num是当前要旋转的数字
                for (int cnt = 0; cnt < 4; cnt++)// 旋转四次即为1周
                {
                	int temp = matrix[j][n-i-1];// temp是被当前要旋转的数字覆盖的数字
                    matrix[j][n-i-1] = num;// 在计算得到的位置放入当前要旋转的数字
                    num = temp;// 下一个要旋转的数字就是当前被覆盖的数字
                    
                    // j->i,n-i-1->j
                    // 因为j->i会改变i的值，所以需要用第三个变量暂存i的值
                    int t = n-i-1;
                    i = j;
                    j = t;
                 }
             }   
        }    
    }
};
```
