#

## 两数之和
https://leetcode.cn/problems/two-sum/description/
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans(2, -1);
        for (int i = 0; i < nums.size()-1; i++) {
            for (int j = i+1; j < nums.size(); j++) {
                if (nums[i] + nums[j] == target) {
                    ans[0] = i;
                    ans[1] = j;
                    return ans;
                }
            }
        }
        return ans;
    }
};
```

## 两数之和 II
https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/description/
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int l = 0, r = numbers.size()-1;
        while (l < r) {
            int sum = numbers[l] + numbers[r];
            if (sum == target) {
                return vector<int>{l+1, r+1};
            } else if (sum < target) {
                l += 1;
            } else if (sum > target) {
                r -= 1;
            }
        }
        return vector<int>{-1, -1};
    }
};
```

## 三数之和
https://leetcode.cn/problems/3sum/
```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end(), 
            [](const int& lhs, const int& rhs) {
                return lhs < rhs;
            });
        vector<vector<int>> ans;
        for (int i = 0; i < nums.size()-2; i++) {
            if (i > 0 && nums[i] == nums[i-1]) // 跳过重复项
                continue;
            int l = i+1, r = nums.size()-1;
            while (l < r) {
                int sum = nums[i] + nums[l] + nums[r];
                if (sum == 0) {
                    ans.push_back(vector<int>{nums[i], nums[l], nums[r]});
                    while (l < r && nums[l] == nums[l+1]) l += 1; // 消除重复项
                    l += 1;
                    while (l < r && nums[r] == nums[r-1]) r -= 1; // 消除重复项
                    r -= 1;
                } else if (sum < 0) {
                    while (l < r && nums[l] == nums[l+1]) l += 1; // 优化性能
                    l += 1;
                } else if (sum > 0) {
                    while (l < r && nums[r] == nums[r-1]) r -= 1; // 优化性能
                    r -= 1;
                }
            }
        }
        return ans;
    }
};
```

## 四数之和
https://leetcode.cn/problems/4sum/
```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums, int beg, int taret) {
        vector<vector<int>> ans;
        for (int i = beg; i < nums.size()-2; i++) {
            if (i > beg && nums[i] == nums[i-1]) // 跳过重复项
                continue;
            int l = i+1, r = nums.size()-1;
            while (l < r) {
                long long sum = (long long)nums[i] + nums[l] + nums[r];
                if (sum == taret) {
                    ans.push_back(vector<int>{nums[i], nums[l], nums[r]});
                    while (l < r && nums[l] == nums[l+1]) l += 1; // 消除重复项
                    l += 1;
                    while (l < r && nums[r] == nums[r-1]) r -= 1; // 消除重复项
                    r -= 1;
                } else if (sum < taret) {
                    while (l < r && nums[l] == nums[l+1]) l += 1; // 优化性能
                    l += 1;
                } else if (sum > taret) {
                    while (l < r && nums[r] == nums[r-1]) r -= 1; // 优化性能
                    r -= 1;
                }
            }
        }
        return ans;
    }
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> ans;
        if (nums.size() < 4)
            return ans;

        sort(nums.begin(), nums.end(), 
            [](const int& lhs, const int& rhs) {
                return lhs < rhs;
            });
        
        for (int i = 0; i < nums.size()-3; i++) {
            if (i > 0 && nums[i] == nums[i-1]) // 跳过重复项
                continue;
            vector<vector<int>> tmp = threeSum(nums, i+1, target-nums[i]);
            for (vector<int>& t : tmp) {
                t.push_back(nums[i]);
                ans.push_back(t);
            }
        }
        return ans;
    }
};
```
