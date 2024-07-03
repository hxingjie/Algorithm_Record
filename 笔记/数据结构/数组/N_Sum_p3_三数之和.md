# 三数之和

给你一个整数数组 `nums` ，判断是否存在三元组 `[nums[i], nums[j], nums[k]]` 满足 `i != j`、`i != k` 且 `j != k` ，同时还满足 `nums[i] + nums[j] + nums[k] == 0` 。请

你返回所有和为 `0` 且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

[15. 三数之和 - 力扣（LeetCode）](https://leetcode.cn/problems/3sum/description/)

```c++
class Solution {
public:
    vector<vector<int>> twoSum(vector<int>& nums, int beg, int target){
        vector<vector<int>> res;
        int l = beg, r = nums.size()-1;
        while (l < r){
            int last_l = nums[l];
            int last_r = nums[r];
            if (nums[l] + nums[r] == target){
                vector<int> temp = {nums[l], nums[r]};
                res.push_back(temp);
                while (l < r && nums[l] == last_l) l++;// 防止重复
                while (l < r && nums[r] == last_r) r--;// 避免不必要的检查
            }else if (nums[l] + nums[r] > target)
            {
                while (l < r && nums[r] == last_r) r--;// 避免不必要的检查
            }else if (nums[l] + nums[r] < target)
            {
                while (l < r && nums[l] == last_l) l++;// 避免不必要的检查
            }
        }
        return res;
    }
    
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        
        vector<vector<int>> res;
        for (int i = 0; i <= nums.size()-3; )// 遍历第1个元素
        {   
            vector<vector<int>> temp = twoSum(nums,i+1,0-nums[i]);
            if (temp.size())
            {
                for (int j = 0; j < temp.size(); j++){
                    temp[j].push_back(nums[i]);
                    res.push_back(temp[j]);
                }
            }
            int last_num = nums[i];
            i++;
            while (i <= nums.size()-3 && nums[i] == last_num) i++;// 第1个元素不能相同
        }
        return res;
    }
};
```

