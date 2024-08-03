# Other

## 按权重随机选择
https://leetcode.cn/problems/random-pick-with-weight/
```c++
/*
*   1     3   2 1
*  _|_ _ _|_ _|_|
* 0 1     4   6 7
* rand num == 1, return idx 0
* rand num == 2,3,4, return idx 1
* rand num == 5,6, return idx 2
* rand num == 7, return idx 3

* std::rand() % preSum.back() + 1; -> [1, preSum.back()]
*/
class Solution {
public:
    vector<int> preSum;
    Solution(vector<int>& w)
        : preSum(vector<int>(w.size(), 0)) {
        preSum[0] = w[0];
        for (int i = 1; i < preSum.size(); i++)
            preSum[i] = preSum[i-1] + w[i];
    }
    
    int pickIndex() {
        int n = preSum.size();
        int val = std::rand() % preSum[n-1] + 1;
        int idx = FoundIdx(val);
        return idx;
    }

    int FoundIdx(int val) {
        int l = 0, r = preSum.size()-1;
        while (l <= r) {
            int mid = l + (r-l)/2;
            if (preSum[mid] == val) return mid;
            else if (preSum[mid] < val) l = mid + 1;
            else if (preSum[mid] > val) r = mid - 1;
        }
        return l;
    }
};
```
