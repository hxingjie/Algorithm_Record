# 组合III

找出所有相加之和为 `n` 的 `k` 个数的组合，且满足下列条件：

- 只使用数字1到9
- 每个数字 **最多使用一次** 

返回 *所有可能的有效组合的列表* 。该列表不能包含相同的组合两次，组合可以以任何顺序返回。

[216. 组合总和 III - 力扣（LeetCode）](https://leetcode.cn/problems/combination-sum-iii/description/)

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    void traverse(int k, int n, int start){
        if (path.size() == k){
            int sum = 0;
            for (int i = 0; i < k; ++i) sum += path[i];
            if (sum == n) ans.push_back(path);
            return;
        }

        for (int i = start; i <= 9; ++i) {
            path.push_back(i);
            traverse(k,n,i+1);
            path.pop_back();
        }
        
    }
    vector<vector<int>> combinationSum3(int k, int n) {// k个数相加为n
        traverse(k,n,1);
        return ans;
    }
};
```

```c#
public class Solution
{
    public IList<IList<int>> ans = new List<IList<int>>();
    public IList<int> path = new List<int>();

    public void Traverse(int k, int n, int start)
    {
        if (path.Count == k)
        {
            int sum = 0;
            foreach (int num in path) sum += num;
            if (sum == n) ans.Add(new List<int>(path));
            return;
        }

        for (int i = start; i <= 9; i++)
        {
            path.Add(i);
            Traverse(k, n, i+1);
            path.Remove(i);
        }
    }
    public IList<IList<int>> CombinationSum3(int k, int n) {
        Traverse(k, n, 1);
        return ans;
    }
}
```

