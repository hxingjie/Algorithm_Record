# Other

## 田忌赛马
https://leetcode.cn/problems/advantage-shuffle/description/
```c++
// 两个数组从小到大排序
// 从大的元素开始比起，nums1对应元素大于nums2对应元素，直接 solo
// 否则，用nums1最小元素当炮灰
// tips: nums1[i] > nums2[i]时没必要尝试用nums1[i-j]去solo，因为nums1[i]留着也没用
class Solution {
public:
    vector<int> advantageCount(vector<int>& nums1, vector<int>& nums2) {
        vector<pair<int, int>> mm;
        for (int i = 0; i < nums2.size(); i++)
            mm.push_back(pair<int, int>(i, nums2[i]));

        sort(nums1.begin(), nums1.end(),
            [](const int &lhs, const int &rhs) {
                return lhs < rhs;
            });
        sort(mm.begin(), mm.end(),
            [](const pair<int, int> &lhs, const pair<int, int> &rhs) {
                return lhs.second < rhs.second;
            });
        
        int pL = 0;
        int pR = nums1.size()-1;
        int p2 = nums2.size()-1;
        vector<int> ans(nums1.size(), -1);
        while (p2 >= 0) {
            int idx = mm[p2].first, val = mm[p2].second;
            if (nums1[pR] > val) {
                ans[idx] = nums1[pR];
                pR -= 1;
            } else {
                ans[idx] = nums1[pL];
                pL += 1;
            }
            p2 -= 1;
        }
        return ans;
    }
};
```

## O(1)时间插入删除获得随即元素
https://leetcode.cn/problems/insert-delete-getrandom-o1/description/
```c++
// 使用数组存储，实现O(1)插入(push_back)
// 移除时将待移除的数字和尾部数字交换，实现O(1)移除(pop_back)
// 为了O(1)找到待移除的数字在数组中的下标，使用map记录元素值和下标的映射
class RandomizedSet {
public:
    vector<int> nums;
    unordered_map<int, int> val2idx;
    RandomizedSet() 
        : nums(vector<int>()), val2idx(unordered_map<int, int>()) {
        
    }
    
    bool insert(int val) {
        if (val2idx.count(val))
            return false; // 已经存在

        nums.push_back(val);
        val2idx[val] = nums.size()-1;
        return true;
    }
    
    bool remove(int val) {
        if (not val2idx.count(val))
            return false; // 不存在该元素

        int idx = val2idx[val];
        swap(nums[idx], nums[nums.size()-1]);
        val2idx[nums[idx]] = idx;
        
        nums.pop_back();
        val2idx.erase(val);
        return true;
    }
    
    int getRandom() {
        int idx = rand() % nums.size();
        return nums[idx];
    }
};
```

## 黑名单中的随机数
https://leetcode.cn/problems/random-pick-with-blacklist/submissions/552379985/
```c++
class Solution {
public:
    int sz;
    unordered_map<int, int> mm;
    Solution(int n, vector<int>& blacklist) : sz(0) {
        sz = n-blacklist.size(); // 选择区间
        // 0 1 (2) (3) | 4 (5) 6
        //      4   6
        // 将2,3映射到4,6
        // 在[0,1,2,3]中随机取数，如果取到0,1直接返回
        // 如果取到2,3返回其映射4,6
        unordered_set<int> blackNums;
        for (int t : blacklist)
            blackNums.insert(t);
        
        int ptr = n-1;
        for (int i = 0; i < blacklist.size(); i++) {
            if (blacklist[i] >= sz)
                continue;
            // [sz,n-1]区间的数字不需要映射，[0, sz) 区间的黑名单数字映射到 [sz, n-1]
            while (blackNums.count(ptr))
                ptr -= 1;
            mm[blacklist[i]] = ptr;
            ptr -= 1;
        }
    }
    
    int pick() {
        int idx = rand()%sz;
        if (mm.count(idx))
            return mm[idx];
        return idx;
    }
};
```
