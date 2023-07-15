# 搜索插入位置

​		给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        // 1 3 5 7
        int l = 0, r= nums.size();
        while (l <= r){
            int mid = (r-l)/2;
            if (target > nums[mid]) l = mid+1;
            else if (target < nums[mid]) r = mid-1;
            else return mid;
        }
        return l;
    }
};
```

