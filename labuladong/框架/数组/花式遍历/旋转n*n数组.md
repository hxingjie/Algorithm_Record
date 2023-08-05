顺时针90度旋转数组
```c#
public class Solution {
    public void Rotate(int[][] matrix) {
        // 1 4 7
        // 2 5 8
        // 3 6 9
        for (int i = 0; i < matrix.Length; i++)// 先将数组按照正对角线交换元素，按照反对角线交换元素即为逆时针90度旋转数组
        {
            for (int j = i; j < matrix[i].Length; j++)
            {
                if (i == j) continue;
                (matrix[i][j], matrix[j][i]) = (matrix[j][i], matrix[i][j]);
            }
        }

        for (int i = 0; i < matrix.Length; i++)// 反转每一行的元素
        {
            int l = 0, r = matrix[i].Length - 1;
            while (l < r)
            {
                (matrix[i][l], matrix[i][r]) = (matrix[i][r], matrix[i][l]);
                l++;
                r--;
            }
        }
    }
}
```
