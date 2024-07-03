# 两数之和II-输入有序数组

给你一个下标从 **1** 开始的整数数组 `numbers` ，该数组已按 **非递减顺序排列** ，请你从数组中找出满足相加之和等于目标数 `target` 的两个数。如果设这两个数分别是 `numbers[index1]` 和 `numbers[index2]` ，则 `1 <= index1 < index2 <= numbers.length` 。

以长度为 2 的整数数组 `[index1, index2]` 的形式返回这两个整数的下标 `index1` 和 `index2`。

你可以假设每个输入 **只对应唯一的答案** ，而且你 **不可以** 重复使用相同的元素。

你所设计的解决方案必须只使用常量级的额外空间。

[167. 两数之和 II - 输入有序数组 - 力扣（LeetCode）](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/description/)

```c++
// 因为是有序数组，所以双指针分别指向最小值和最大值，左值针向右、右指针向左找答案
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        vector<int> res;

        int l = 0, r = numbers.size()-1;
        while (l < r){
            int sum = numbers[l] + numbers[r];
            if (sum < target){
                l++;
            }else if (sum > target){
                r--;
            }else{// found the res
                res.push_back(l+1);
                res.push_back(r+1);
                break;
            }
        }

        return res;
    }
};
```

