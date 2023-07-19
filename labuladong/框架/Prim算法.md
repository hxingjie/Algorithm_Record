Prim算法

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

