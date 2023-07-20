# 前K个高频元素

给你一个整数数组 `nums` 和一个整数 `k` ，请你返回其中出现频率前 `k` 高的元素。你可以按 **任意顺序** 返回答案。

[347. 前 K 个高频元素 - 力扣（LeetCode）](https://leetcode.cn/problems/top-k-frequent-elements/description/)

```c++
// 先从哈希表存储元素
// 在使用优先级队列以得到频率最高的元素
class Solution {
public:
    class cmpClass{
    public:
        bool operator () (const pair<int,int> &lhs, const pair<int,int> &rhs) const{
            if (lhs.second < rhs.second) return true;
            else return false;
        }
    };
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int> m;
        for (int i = 0; i < nums.size(); i++)
        {
            if (m.count(nums[i]))
            {
                m[nums[i]]++;
            }else{
                m[nums[i]] = 1;
            }
        }
        priority_queue<pair<int,int>,vector<pair<int,int>>,cmpClass> pq;
        unordered_map<int,int>::iterator it = m.begin();
        while (it != m.end()){
            pq.push(*it);
            it++;
        }
        
        vector<int> res;
        for (int i = 0; i < k; i++){
            res.push_back(pq.top().first);
            pq.pop();
        }
        return res;
    }
};
```

```c#
public class Solution
    {
        public class MyCompare : IComparer<int>
        {
            public int Compare(int lhs, int rhs)
            {
                return rhs - lhs;
            }
        }
        public int[] TopKFrequent(int[] nums, int k)
        {
            Dictionary<int, int> dict = new Dictionary<int, int>();
            for (int i = 0; i < nums.Length; i++)// 建立哈希表
            {
                if (dict.ContainsKey(nums[i])) dict[nums[i]]++;
                else dict.Add(nums[i], 1);
            }

            MyCompare myCompare = new MyCompare();
            PriorityQueue<int, int> pq = new PriorityQueue<int, int>(myCompare);
            
            // 迭代方式1
            foreach (KeyValuePair<int,int> pair in dict)
                pq.Enqueue(pair.Key, pair.Value);
            // 迭代方式2
            for (int i = 0; i < dict.Count; i++)
            	pq.Enqueue(dict.ElementAt(i).Key,dict.ElementAt(i).Value);  

            List<int> list = new List<int>();
            for (int i = 0;i < k; i++) list.Add(pq.Dequeue());

            int[] res = list.ToArray<int>();
            return res;
        }
    }
```

