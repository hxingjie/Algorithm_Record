# 四数之和

给你一个由 `n` 个整数组成的数组 `nums` ，和一个目标值 `target` 。请你找出并返回满足下述全部条件且**不重复**的四元组 `[nums[a], nums[b], nums[c], nums[d]]` （若两个四元组元素一一对应，则认为两个四元组重复）：

[18. 四数之和 - 力扣（LeetCode）](https://leetcode.cn/problems/4sum/description/)

```c++
class Solution {
public:
    vector<vector<int>> twoSum(vector<int>& nums, int beg, long long target){
        vector<vector<int>> res;
        int l = beg, r = nums.size()-1;
        while (l < r){
            int last_l = nums[l];
            int last_r = nums[r];
            long long sum = nums[l] + nums[r];
            if (sum == target){
                vector<int> temp = {nums[l], nums[r]};
                res.push_back(temp);
                while (l < r && nums[l] == last_l) l++;// 防止重复
                while (l < r && nums[r] == last_r) r--;// 避免不必要的检查
            }else if (sum > target)
            {
                while (l < r && nums[r] == last_r) r--;// 避免不必要的检查
            }else if (sum < target)
            {
                while (l < r && nums[l] == last_l) l++;// 避免不必要的检查
            }
        }
        return res;
    }
    
    vector<vector<int>> threeSum(vector<int>& nums, int beg, long long target) {
        vector<vector<int>> res;
        for (int i = beg; i <= nums.size()-3; )// 遍历第1个元素
        {   
            vector<vector<int>> temp = twoSum(nums,i+1,(long long)(target-nums[i]));
            if (temp.size())
            {
                for (int j = 0; j < temp.size(); j++){
                    temp[j].push_back(nums[i]);
                    res.push_back(temp[j]);
                }
            }
            int last_num = nums[i];
            while (i <= nums.size()-3 && nums[i] == last_num) i++;// 第1个元素不能相同
        }
        return res;
    }

    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> res;
        if (nums.size() < 4) return res;

        sort(nums.begin(), nums.end());
        
        for (int i = 0; i <= nums.size()-4; )
        {
            vector<vector<int>> temp = threeSum(nums, i+1, (long long)target-nums[i]);
            if (temp.size())
            {
                for (int j = 0; j < temp.size(); j++)
                {
                    temp[j].push_back(nums[i]);
                    res.push_back(temp[j]);
                }
            }
            int last_num = nums[i];
            while (i <= nums.size()-4 && nums[i] == last_num) i++;
        }
        return res;   
    }
};
```

