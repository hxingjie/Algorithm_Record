# 子集II

给你一个整数数组 `nums` ，其中可能包含重复元素，请你返回该数组所有可能的子集（幂集）。

解集 **不能** 包含重复的子集。返回的解集中，子集可以按 **任意顺序** 排列。

[90. 子集 II - 力扣（LeetCode）](https://leetcode.cn/problems/subsets-ii/description/)

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> track;
    void backTrack(vector<int>& nums, int beg){
        ans.push_back(track);

        for (int i = beg; i < nums.size(); ++i) {
            if (i > beg && nums[i] == nums[i-1]) continue;// 树枝去重
            track.push_back(nums[i]);
            backTrack(nums,i+1);
            track.pop_back();
        }
    }
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        backTrack(nums,0);
        return ans;
    }
};
```

```c#
public class Solution
    {
        public IList<IList<int>> ans = new List<IList<int>>();
        public IList<int> track = new List<int>();
        public void BackTrack(int[] nums, int beg)
        {
            ans.Add(new List<int>(track));

            for (int i = beg; i < nums.Length; i++)
            {
                if (i > beg && nums[i] == nums[i-1]) continue;
                track.Add(nums[i]);
                BackTrack(nums,i+1);
                track.RemoveAt(track.Count-1);
            }
        }
        public IList<IList<int>> SubsetsWithDup(int[] nums)
        {
            List<int> list = new List<int>(nums);
            list.Sort();
            BackTrack(list.ToArray(),0);
            return ans;
        }
    }
```

