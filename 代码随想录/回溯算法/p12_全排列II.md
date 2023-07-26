# 全排列II

给定一个可包含重复数字的序列 `nums` ，***按任意顺序*** 返回所有不重复的全排列。

[47. 全排列 II - 力扣（LeetCode）](https://leetcode.cn/problems/permutations-ii/description/)

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> track;
    vector<bool> used;
    void backTrack(vector<int>& nums){
        if (track.size() == nums.size()){
            ans.push_back(track);
            return;
        }
        
        set<int> hasPick;
        for (int i = 0; i < nums.size(); ++i) {
            if (used[i] == true) continue; // track has nums[i]
            if (hasPick.count(nums[i])) continue;
            hasPick.insert(nums[i]);
            track.push_back(nums[i]);
            used[i] = true;
            backTrack(nums);
            track.pop_back();
            used[i] = false;
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        used = vector<bool>(nums.size(),false);
        backTrack(nums);
        return ans;
    }
};
```

```c#

```

