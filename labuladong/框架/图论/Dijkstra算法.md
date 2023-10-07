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
---
```c++
class Path{
public:
    int end_id;
    int dist; // start to cur
    Path(int a, int b) : end_id(a), dist(b) { }
};

int main(){
    int n, m;
    cin >> n >> m;
    vector<vector<pair<int,int>>> graph(n+1);
    for (int i = 0; i < m; ++i) {
        int from, to, weight;
        scanf("%d %d %d", &from, &to, &weight);
        graph[from].push_back(pair<int,int>(to, weight));
    }

    vector<int> dist(n+1, INT_MAX); // start到i的当前最短距离

    dist[1] = 0;

    queue<Path> q;
    q.push(Path(1, 0));
    while (!q.empty()){
        Path cur = q.front();
        q.pop();

        if (cur.dist > dist[cur.end_id]) continue;// 小于或等于都继续

        for (pair<int,int> edge : graph[cur.end_id]) {
            int to = edge.first;
            int weight = edge.second;
            if (cur.dist + weight < dist[to]){
                dist[to] = cur.dist + weight;
                q.push(Path(to, cur.dist + weight));
            }
        }

    }

    printf("%d\n", dist[n] == INT_MAX ? -1 : dist[n]);
    
    return 0;
}
```
