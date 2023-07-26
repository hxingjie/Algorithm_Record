# 组合总和II

给定一个候选人编号的集合 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的每个数字在每个组合中只能使用 **一次** 。

**注意：**解集不能包含重复的组合。 

[40. 组合总和 II - 力扣（LeetCode）](https://leetcode.cn/problems/combination-sum-ii/description/)

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    void traverse(vector<int>& candidates, int target, int start, int sum){
        if (sum == target){
            ans.push_back(path);
            return;
        }else if (sum > target){
            return;
        }
        set<int> used;
        for (int i = start; i < candidates.size(); ++i) {
            //
            if (used.count(candidates[i]) > 0) continue;
            used.insert(candidates[i]);
            path.push_back(candidates[i]);
            traverse(candidates, target, i+1, sum+candidates[i]);
            path.pop_back();
        }
    }
    
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        traverse(candidates, target, 0, 0);
        return ans;
    }
};
```

```c#
public class Solution
{
    public IList<IList<int>> ans = new List<IList<int>>();
    public IList<int> path = new List<int>();

    public void Traverse(List<int> candidates, int target, int start, int sum)
    {
        if (sum == target)
        {
            ans.Add(new List<int>(path));
            return;
        }else if (sum > target)
        {
            return;
        }

        for (int i = start; i < candidates.Count; i++)
        {
            if (i > start && candidates[i] == candidates[i-1]) continue;

            path.Add(candidates[i]);
            Traverse(candidates, target, i+1, sum+candidates[i]);
            path.RemoveAt(path.Count-1);
        }
            
    }
    public IList<IList<int>> CombinationSum2(int[] candidates, int target)
    {
        List<int> list = new List<int>(candidates);
        list.Sort();
        Traverse(list, target, 0, 0);
        return ans;
    }
}
```

