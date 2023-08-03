# 下一个更大元素II

给定一个循环数组 `nums` （ `nums[nums.length - 1]` 的下一个元素是 `nums[0]` ），返回 *`nums` 中每个元素的 **下一个更大元素*** 。

数字 `x` 的 **下一个更大的元素** 是按数组遍历顺序，这个数字之后的第一个比它更大的数，这意味着你应该循环地搜索它的下一个更大的数。如果不存在，则输出 `-1` 。

[503. 下一个更大元素 II - 力扣（LeetCode）](https://leetcode.cn/problems/next-greater-element-ii/description/)

```c++
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        // 1,2,3,4,3 1,2,3,4,3
        stack<int> st;
        vector<int> ans(nums.size());
        for (int i = 2*nums.size()-1; i >= 0; --i) {
            while (!st.empty() && st.top() <= nums[i%nums.size()])
                st.pop();
            
            ans[i%nums.size()] = !st.empty() ? st.top() : -1;
            st.push(nums[i%nums.size()]);
            
        }
        return ans;
    }
};
```

