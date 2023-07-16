# 对角线遍历

​		给你一个大小为 `m x n` 的矩阵 `mat` ，请以对角线遍历的顺序，用一个数组返回这个矩阵中的所有元素。

​		[498. 对角线遍历 - 力扣（Leetcode）](https://leetcode.cn/problems/diagonal-traverse/)

```c++
// 斜向上遍历：row-1,col+1
// 斜向下遍历：row+1,col-1

// 重点是要区分同一方向的两种情况
// 向上遍历时，两种情况的区分点在于col，当前的访问的下标不合法时，如果col < m，行列下标应该：row++; 如果col == m，行列下标应该：row += 2, col--;
// 向下遍历时，两种情况的区分点在于row，当前的访问的下标不合法时，如果row < n，行列下标应该：col++; 如果row == n，行列下标应该：row--, col += 2;
class Solution {
public:
    vector<int> findDiagonalOrder(vector<vector<int>>& mat) {
        vector<int> res;

        int n = mat.size(), m = mat[0].size();
        int direct = 1; // direct定义为：0为向上，1为向下
        int row = 0, col = 0;
        // 向上：row-1,col+1; 向下：row+1,col-1
        while (true)
        {
            if (direct == 1)
            {
                while (row >= 0 && col < m){
                    res.push_back(mat[row][col]);
                    if (row == n-1 && col == m-1)
                    {
                        return res;
                    }
                    row--, col++;
                }
                if (col == m) { row += 2, col--; }
                else { row++; }
                direct = 0;
            }else{
                while (row < n && col >= 0){
                    res.push_back(mat[row][col]);
                    if (row == n-1 && col == m-1)
                    {
                        return res;
                    }
                    row++, col--;
                }
                if (row < n) { col++; }
                else { row--, col += 2; }
                direct = 1;
            }
        }
    }
};
```

