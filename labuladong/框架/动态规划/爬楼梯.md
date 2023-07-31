# 组合总和IV

给你一个由 **不同** 整数组成的数组 `nums` ，和一个目标整数 `target` 。请你从 `nums` 中找出并返回总和为 `target` 的元素组合的个数。

题目数据保证答案符合 32 位整数范围。

```c++
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        // 爬楼梯问题
        // dp[i]: 总和为target的排列
        // dp[i] = dp[i-nums[0]] + dp[i-nums[1]] + dp[i-nums[...]]
        
        vector<int> dp(target+1);
        dp[0] = 1;
        for (int i = 1; i <= target; ++i) {
            for (int j = 0; j < nums.size(); ++j) {
                if (i >= nums[j] && dp[i] <= INT_MAX - dp[i-nums[j]])
                    dp[i] += dp[i-nums[j]];
            }
        }
        return dp[target];
    }
};
```

```c#
public class Solution {
    public int CombinationSum4(int[] nums, int target)
    {
        int[] dp = new int[target+1];
        dp[0] = 1;
        for (int i = 1; i <= target; i++)
        {
            int sum = 0;
            for (int j = 0; j < nums.Length; j++)
                if (i >= nums[j])
                    sum += dp[i - nums[j]];
            dp[i] = sum;
        }

        return dp[target];
    }
}
```

