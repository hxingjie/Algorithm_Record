# 零钱兑换II

给你一个整数数组 `coins` 表示不同面额的硬币，另给一个整数 `amount` 表示总金额。

请你计算并返回可以凑成总金额的硬币组合数。如果任何硬币组合都无法凑出总金额，返回 `0` 。

假设每一种面额的硬币有无限个。 

题目数据保证结果符合 32 位带符号整数。

[518. 零钱兑换 II - 力扣（LeetCode）](https://leetcode.cn/problems/coin-change-ii/description/)

```c++
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        // 定义：dp[i][j]:前i种面额的硬币凑出j块钱的方式数
        // 根据定义得出递推式：dp[i][j] = dp[i-1][j] + dp[i][j-coins[i-1]]
        // 根据递推式得出遍历顺序：i min -> max，j min -> max
        // 根据遍历顺序得出初始值设置：dp[0][0] = 1, dp[0][1->amount] = 0
        
        int n = coins.size();
        vector<vector<int>> dp(n+1, vector<int>(amount+1,0));
        dp[0][0] = 1;
        
        for (int i = 1; i <= n; ++i) {
            for (int j = 0; j <= amount; ++j) {
                if (j >= coins[i-1])
                    dp[i][j] = dp[i-1][j] + dp[i][j-coins[i-1]];
                else
                    dp[i][j] = dp[i-1][j];
            }
        }
        return dp[n][amount];
    }
};
```

```c#
public class Solution {
            public int Change(int amount, int[] coins)
            {

                int n = coins.Length;
                int[,] dp = new int[n + 1, amount + 1];
                dp[0, 0] = 1;
                
                for (int i = 1; i <= n; i++)
                {
                    for (int j = 0; j <= amount; j++)
                    {
                        if (j >= coins[i - 1])
                            dp[i, j] = dp[i - 1, j] + dp[i, j - coins[i - 1]];
                        else
                            dp[i, j] = dp[i - 1, j];
                    }
                }

                return dp[n, amount];
            }
        }
```

