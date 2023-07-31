## 打家劫舍II

你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都 **围成一圈** ，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警** 。

给定一个代表每个房屋存放金额的非负整数数组，计算你 **在不触动警报装置的情况下** ，今晚能够偷窃到的最高金额。

[213. 打家劫舍 II - 力扣（LeetCode）](https://leetcode.cn/problems/house-robber-ii/description/)

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 1) return nums[0];

        // 因为是第0家和最后一家是相邻的，所以：
        // 1.第0家和最后一家都不选择
        // 2.第0家都不选择
        // 3.最后一家都不选择

        // 2和3的结果肯定大于1，只考虑2和3

        // dp[i]: 从第i家开始选择所偷得的最大金额
        int ans = -1;
        
        vector<int> dp(nums.size()+2, 0);
        
        dp[nums.size()] = 0;
        dp[nums.size()+1] = 0;
        for (int i = nums.size()-1; i > 0; --i) {// 不选择i==0
            dp[i] = max(dp[i+1], dp[i+2] + nums[i]);
        }
        ans = dp[1];
        
        dp[nums.size()-1] = 0;
        dp[nums.size()] = 0;
        for (int i = nums.size()-2; i >= 0; --i) {// 不选择i==nums.size()-1
            dp[i] = max(dp[i+1], dp[i+2] + nums[i]);
        }
        ans = max(ans,dp[0]);
        return ans;
    }
};
```

```c#
public class Solution {
    public int Rob(int[] nums)
    {
        if (nums.Length == 1) return nums[0];

        int n = nums.Length;
        int ans = -1;
        int[] dp = new int[n + 2];
            
        dp[n] = 0;
        dp[n + 1] = 0;
        for (int i = n-1; i > 0; i--)
            dp[i] = Math.Max(dp[i + 1], dp[i + 2] + nums[i]);
        ans = dp[1];

        dp[n - 1] = 0;
        dp[n] = 0;
        for (int i = n - 2; i >= 0; i--)
            dp[i] = Math.Max(dp[i + 1], dp[i + 2] + nums[i]);
        ans = Math.Max(ans, dp[0]);

        return ans;
    }
}
```
