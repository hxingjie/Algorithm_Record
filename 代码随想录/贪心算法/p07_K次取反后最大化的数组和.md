# K次取反后最大化的数组和

给你一个整数数组 `nums` 和一个整数 `k` ，按以下方法修改该数组：

- 选择某个下标 `i` 并将 `nums[i]` 替换为 `-nums[i]` 。

重复这个过程恰好 `k` 次。可以多次选择同一个下标 `i` 。

以这种方式修改数组后，返回数组 **可能的最大和** 。

[1005. K 次取反后最大化的数组和 - 力扣（LeetCode）](https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/)

```c++
class Solution {
public:
    int largestSumAfterKNegations(vector<int>& nums, int k) {
        
        for (int i = 0; i < k; ++i) {
            int minVal = INT_MAX, minValPos;
            for (int j = 0; j < nums.size(); ++j) {
                if (nums[j] < minVal){
                    minVal = nums[j];
                    minValPos = j;
                }
            }
            nums[minValPos] *= -1;
        }
        int sum = 0;
        for (int i = 0; i < nums.size(); ++i) {
            sum += nums[i];
        }
        return sum;
    }
};
```

```c#
public class Solution {
    public int Sum(List<int> list)
    {
        int sum = 0;
        for (int i = 0; i < list.Count; i++) sum += list[i];
        return sum;
    }
    public int LargestSumAfterKNegations(int[] nums, int k)
    {
        List<int> list = new List<int>(nums);
        list.Sort();// -3 -2 -1
                
        for (int j = 0; j < list.Count; j++)
        {
            if (list[j] < 0)
            {
                list[j] *= -1;
                k--;
                if (k == 0) return Sum(list);// 次数用完了
            }
            else break;// 负数翻转完了
        }
                
        // list中只剩下大于等于的数
        list.Sort();
        if (k % 2 != 0) list[0] *= -1;
            
        return Sum(list);
    }
}
```

