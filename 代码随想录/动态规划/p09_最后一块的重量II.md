# 最后一块的重量II

有一堆石头，用整数数组 `stones` 表示。其中 `stones[i]` 表示第 `i` 块石头的重量。

每一回合，从中选出**任意两块石头**，然后将它们一起粉碎。假设石头的重量分别为 `x` 和 `y`，且 `x <= y`。那么粉碎的可能结果如下：

- 如果 `x == y`，那么两块石头都会被完全粉碎；
- 如果 `x != y`，那么重量为 `x` 的石头将会完全粉碎，而重量为 `y` 的石头新重量为 `y-x`。

最后，**最多只会剩下一块** 石头。返回此石头 **最小的可能重量** 。如果没有石头剩下，就返回 `0`。

[1049. 最后一块石头的重量 II - 力扣（LeetCode）](https://leetcode.cn/problems/last-stone-weight-ii/description/)

```c++
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        // 23 /= 2 -> 11, 12
        int sum = 0;
        for (int i = 0; i < stones.size(); ++i) {
            sum += stones[i];
        }
        int ssum = sum;
        sum /= 2;
        
        // dp[i][j]: 前i块石头是否能凑出和为j的重量
        vector<vector<int>> dp(stones.size()+1, vector<int>(1505));

        // dp[0][0]应该置为true
        dp[0][0] = true;
        for (int j = 1; j <= sum; ++j)
            dp[0][j] = false;
        
        for (int i = 1; i <= stones.size(); ++i) {
            for (int j = 0; j <= sum; ++j) {
                if (j >= stones[i-1])
                    dp[i][j] = dp[i-1][j] || dp[i-1][j-stones[i-1]];
                else
                    dp[i][j] = dp[i-1][j];
            }
        }
        int res = -1;
        for (int i = sum; i >= 0; i--){
            if (dp[stones.size()][i] == true){
                res = (ssum - i) - i;
                break;
            }
        }
        return res;
    }
};
```

```c#
public class Solution {
    public int LastStoneWeightII(int[] stones)
    {
        int n = stones.Length;
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += stones[i];
        
        int sSum = sum;
        sum /= 2;
        
      	// dp[i,j]: 使用前i个石头是否能凑出重量为j的石头堆
        bool[,] dp = new bool[n + 1, sum + 1];
        // dp[i,j] = dp[i-1,j] || dp[i-1,j-stones[i-1]]
        dp[0, 0] = true;
        for (int j = 1; j <= sum; j++)
            dp[0, j] = false;

        for (int i = 1; i <= n; i++)
        {
            for (int j = 0; j <= sum; j++)
            {
                if (j >= stones[i - 1])
                    dp[i, j] = dp[i - 1, j] || dp[i - 1, j - stones[i - 1]];
                else
                    dp[i, j] = dp[i - 1, j];
            }
        }

        int res = -1;
        for (int i = sum; i >= 0; i--)
        {
            if (dp[n, i] == true)
            {
                res = sSum - i - i;
                break;
            }
        }

        return res;
    }
}
```

