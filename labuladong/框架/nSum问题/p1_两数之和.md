# 两数之和

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

```c++
// 暴搜
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> res;
        
        for (int i = 0; i < nums.size(); i++){
            for (int j = i+1; j < nums.size(); j++){
                if (nums[i] + nums[j] == target){
                    res.push_back(i);
                    res.push_back(j);
                    break;
                }
            }
        }

        return res;
    }
};
```

```c++
// 哈希表
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> res;
        
        map<int,int> mem;// val,int
        for (int idx = 0; idx < nums.size(); idx++){
            int temp = nums[idx];
            if (mem.count(target-temp)){
                res.push_back(mem[target-temp]);
                res.push_back(idx);
                break;
            }else{
                mem[nums[idx]] = idx;
            }
        }

        return res;
    }
};
```

