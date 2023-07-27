# 买卖股票的最佳时机II

给你一个整数数组 `prices` ，其中 `prices[i]` 表示某支股票第 `i` 天的价格。

在每一天，你可以决定是否购买和/或出售股票。你在任何时候 **最多** 只能持有 **一股** 股票。你也可以先购买，然后在 **同一天** 出售。

返回 *你能获得的 **最大** 利润* 。

[122. 买卖股票的最佳时机 II - 力扣（LeetCode）](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/description/)

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        // dp[i][1]
        // dp[i][0]
        vector<vector<int>> dp(prices.size(), vector<int>(2));

        for (int i = 0; i < prices.size(); ++i) {
            if (i == 0){
                dp[i][0] = 0;
                dp[i][1] = 0-prices[i];
            }else{
                dp[i][0] = max(dp[i-1][0], dp[i-1][1]+prices[i]);
                dp[i][1] = max(dp[i-1][1], dp[i-1][0]-prices[i]);
            }
        }
        return dp[prices.size()-1][0];
    }
};
```

```c#
public class Solution {
    public int MaxProfit(int[] prices)
    {
        int[,] dp = new int[prices.Length, 2];

        for (int i = 0; i < prices.Length; i++)
        {
            if (i == 0)
            {
                dp[i,0] = 0;
                dp[i,1] = 0 - prices[i];
            }
            else
            {
                dp[i,0] = max(dp[i-1,0], dp[i-1,1]+prices[i]);
                dp[i,1] = max(dp[i-1,1], dp[i-1,0]-prices[i]);
            }
        }

        return dp[prices.Length - 1,0];
    }
}
```

