Prim算法
```c++
class Edge{
public:
    int from;
    int to;
    int weight;
    Edge(int a, int b, int c) : from(a), to(b), weight(c) { }
};
class cmp{
public:
    bool operator () (const Edge &lhs, const Edge &rhs) const{
        if (lhs.weight > rhs.weight)
            return true;
        else
            return false;
    }
};
int main(){
    int n, m;
    cin >> n >> m;
    vector<vector<Edge>> graph(n+1);
    for (int i = 0; i < m; ++i) {
        int u, v, w;
        scanf("%d %d %d", &u, &v, &w);
        if (u == v) continue;
        graph[u].push_back(Edge(u, v, w));// 无向边
        graph[v].push_back(Edge(v, u, w));// 无向边
    }

    int ans = 0;
    set<int> visited;
    priority_queue<Edge, vector<Edge>, cmp> pq;
    for (int i = 1; i < graph.size(); ++i) {
        if (graph[i].size() > 0){
            for (int j = 0; j < graph[i].size(); ++j) {
                if (visited.count(graph[i][j].to)) continue;
                pq.push(Edge(graph[i][j].from, graph[i][j].to, graph[i][j].weight));
            }
            visited.insert(i);
            break;
        }
    }

    while (!pq.empty()){
        Edge cur = pq.top();
        pq.pop();

        if (visited.count(cur.to)) continue;// 必须判断，该边加入时to还没有被访问，不代表现在取出时to仍然没有被访问

        visited.insert(cur.to);
        ans += cur.weight;

        for (Edge edge : graph[cur.to]) {
            if (visited.count(edge.to)) continue;
            pq.push(edge);
        }
    }

    if (visited.size() == n)
        printf("%d\n", ans);
    else
        printf("impossible\n");

    return 0;
}
```
---
```c++
#include <iostream>
#include <cstdio>
#include <string>
#include <vector>
#include <queue>
#include <list>
using namespace std;

struct edge{
    int from;
    int to;
    int weight;
    edge(int a, int b, int c)
        :from(a), to(b), weight(c)
    {

    }
};

bool operator < (edge lhs, edge rhs){
    if (lhs.weight > rhs.weight){
        return true;
    }else{
        return false;
    }
}

priority_queue<edge> pq;
vector<bool> inMST(5,false);
int weightSum = 0;
vector<vector<edge>> graph;

void Prim(){
    inMST[0] = true;

    vector<edge> edges = graph[0];
    for (int i = 0; i < edges.size(); ++i) {
        int to = edges[i].to;
        if (inMST[to] == true){
            continue;
        }
        pq.push(edges[i]);
    }

    while (pq.empty() == false){
        edge e = pq.top();
        pq.pop();

        if (inMST[e.to] == true){
            continue;
        }
        cout << e.from << "-->" << e.to << ' ' << e.weight << endl;
        weightSum += e.weight;
        inMST[e.to] = true;

        vector<edge> edges = graph[e.to];
        for (int i = 0; i < edges.size(); ++i) {
            int to = edges[i].to;
            if (inMST[to] == true){
                continue;
            }
            pq.push(edges[i]);
        }
    }
}

int main(){
    vector<edge> temp;
    edge e(0,1,1);
    temp.push_back(e);
    e.from = 0; e.to = 5, e.weight = 6;
    temp.push_back(e);
    graph.push_back(temp);
    temp.clear();

    e.from = 1; e.to = 0, e.weight = 1;
    temp.push_back(e);
    e.from = 1; e.to = 2, e.weight = 2;
    temp.push_back(e);
    e.from = 1; e.to = 3, e.weight = 3;
    temp.push_back(e);
    graph.push_back(temp);
    temp.clear();

    e.from = 2; e.to = 1, e.weight = 2;
    temp.push_back(e);
    e.from = 2; e.to = 3, e.weight = 5;
    temp.push_back(e);
    graph.push_back(temp);
    temp.clear();

    e.from = 3; e.to = 1, e.weight = 3;
    temp.push_back(e);
    e.from = 3; e.to = 2, e.weight = 5;
    temp.push_back(e);
    e.from = 3; e.to = 5, e.weight = 7;
    temp.push_back(e);
    graph.push_back(temp);
    temp.clear();

    e.from = 5; e.to = 0, e.weight = 6;
    temp.push_back(e);
    e.from = 5; e.to = 3, e.weight = 7;
    temp.push_back(e);
    graph.push_back(temp);
    temp.clear();

    Prim();

    return 0;
}
```

