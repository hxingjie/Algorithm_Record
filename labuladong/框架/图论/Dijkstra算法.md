```c++
vector<int> dist(n+1, INT_MAX);
priority_queue<Path, vector<Path>, cmp> pq;
pq.push(Path(k, 0));
dist[k] = 0;

while (!pq.empty()){
    Path cur = pq.top();
    pq.pop();

    if (cur.dist > dist[cur.end_id]) continue;

    for (int i = 0; i < graph[cur.end_id].size(); ++i) {
        int to = graph[cur.end_id][i].first;
        int weight = graph[cur.end_id][i].second;
        if (cur.dist + weight < dist[to]){
            dist[to] = cur.dist + weight;
            pq.push(Path(to, dist[to]));
        }
    }
}
```
---
```c++
class Solution {
public:
    class Path{
    public:
        int end_id;
        int dist;
        Path(int _id, int _dist) : end_id(_id), dist(_dist) {}
    };
    class cmp{
    public:
        bool operator () (const Path &l, const Path &r) const{
            return l.dist > r.dist;
        }
    };
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        vector<vector<pair<int, int>>> graph(n+1);
        for (int i = 0; i < times.size(); ++i) {
            graph[times[i][0]].push_back(pair<int, int>(times[i][1], times[i][2]));
        }

        vector<int> dist(n+1, INT_MAX);
        priority_queue<Path, vector<Path>, cmp> pq;
        pq.push(Path(k, 0));
        dist[k] = 0;

        while (!pq.empty()){
            Path cur = pq.top();
            pq.pop();

            if (cur.dist > dist[cur.end_id]) continue;

            for (int i = 0; i < graph[cur.end_id].size(); ++i) {
                int to = graph[cur.end_id][i].first;
                int weight = graph[cur.end_id][i].second;
                if (cur.dist + weight < dist[to]){
                    dist[to] = cur.dist + weight;
                    pq.push(Path(to, dist[to]));
                }
            }
        }
        int ans = -1;
        for (int i = 1; i < dist.size(); i++){
            ans = max(ans, dist[i]);
        }

        return ans == INT_MAX ? -1 : ans;

    }
};
```
