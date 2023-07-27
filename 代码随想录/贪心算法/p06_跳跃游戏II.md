# 跳跃游戏II

给定一个长度为 `n` 的 **0 索引**整数数组 `nums`。初始位置为 `nums[0]`。

每个元素 `nums[i]` 表示从索引 `i` 向前跳转的最大长度。换句话说，如果你在 `nums[i]` 处，你可以跳转到任意 `nums[i + j]` 处:

- `0 <= j <= nums[i]` 
- `i + j < n`

返回到达 `nums[n - 1]` 的最小跳跃次数。生成的测试用例可以到达 `nums[n - 1]`。

[45. 跳跃游戏 II - 力扣（LeetCode）](https://leetcode.cn/problems/jump-game-ii/description/)

```c++
// 动态规划
class Solution {
public:
    int jump(vector<int>& nums) {
        vector<int> dp(nums.size());
        // dp[i]: 到nums[i]的最小步数
        for (int i = 0; i < nums.size(); ++i) {
            if (i == 0){
                dp[i] = 0;
            }else{
                int minPace = INT_MAX;
                for (int j = i-1; j >= 0; --j) {
                    if (j+nums[j]>=i){// 如果 j 可以跳跃到 i ，就检查是否更新最小步数
                        minPace = min(minPace, dp[j]+1);
                    }
                }
                dp[i] = minPace;
            }
        }
        return dp[nums.size()-1];
    }
};
```

```c#
public class Solution {
            public int Jump(int[] nums)
            {
                int[] dp = new int[nums.Length];
                for (int i = 0; i < nums.Length; i++)
                {
                    if (i == 0) dp[i] = 0;
                    else
                    {
                        int minPace = Int32.MaxValue;
                        for (int j = i-1; j >= 0; j--)
                            if (j + nums[j] >= i)
                                minPace = Math.Min(minPace, dp[j] + 1);
                        dp[i] = minPace;
                    }
                }
                return dp[nums.Length - 1];
            }
        }
```

