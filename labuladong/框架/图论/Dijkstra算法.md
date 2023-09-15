```c++
class Solution {
public:
    class Node{
    public:
        int id;
        int dist;
        Node(int _id, int _dist) : id(_id), dist(_dist) {}
    };
    class cmp{
    public:
        bool operator () (const Node &l, const Node &r) const{
            return l.dist > r.dist;
        }
    };
    vector<int> networkDelayTime(vector<vector<int>>& times, int n, int k) {
        vector<vector<pair<int, int>>> graph(n+1);
        for (int i = 0; i < times.size(); ++i) {
            graph[times[i][0]].push_back(pair<int, int>(times[i][1], times[i][2]));
        }
        vector<int> dist = dijkstra(graph, int k);
        return dist;
    }
    vector<int> dijkstra(vector<vector<pair<int, int>>> &graph, int k){
        vector<int> dist(n+1, INT_MAX);
        priority_queue<Node, vector<Node>, cmp> pq;
        pq.push(Node(k, 0));
        dist[k] = 0;

        while (!pq.empty()){
            int cur = pq.top();
            pq.pop();

            if (cur.dist > dist[cur.id]) continue;
            
            for (int i = 0; i < graph[cur.id].size(); ++i) {
                int to = graph[cur.id][i].first;
                int weight = graph[cur.id][i].second;
                if (cur.dist + weight < dist[to]){
                    dist[to] = cur.dist + weight;
                    pq.push(Node(to, dist[to]));
                }
            }
        }
        return dist;
    }
};
```
