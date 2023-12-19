```c++
class UF{
public:
    vector<int> parents;
    UF(int n){
        parents = vector<int>(n+1);
        for (int i = 0; i <= n; ++i)
            parents[i] = i;
    }
    int find_root(int n){
        if (parents[n] != n){
            parents[n] = find_root(parents[n]);
        }
        return parents[n];
    }
    void union_node(int lhs, int rhs){
        int root1 = find_root(lhs);
        int root2 = find_root(rhs);
        if (root1 != root2){
            parents[root2] = root1;
        }
    }
};
class Edge{
public:
    int from;
    int to;
    int weight;
    Edge(int a, int b, int c) : from(a), to(b), weight(c) { }
};
class cmp{
public:
    bool operator () (const Edge &lhs, const Edge &rhs){
        if (lhs.weight < rhs.weight)
            return true;
        else
            return false;
    }
};
int main(){
    int n, m;
    cin >> n >> m;
    vector<Edge> edges;
    for (int i = 0; i < m; ++i) {
        int u, v, w;
        scanf("%d %d %d", &u, &v, &w);
        edges.push_back(Edge(u, v, w));
    }

    sort(edges.begin(), edges.end(), cmp());

    int ans = 0;
    UF uf(n);
    for (Edge edge : edges) {
        if (uf.find_root(edge.from) != uf.find_root(edge.to)){
            ans += edge.weight;
            uf.union_node(edge.from, edge.to);
        }
    }

    int root = uf.find_root(uf.parents[1]);
    for (int i = 2; i < uf.parents.size(); ++i) {
        if (uf.find_root(uf.parents[i]) != root){
            printf("impossible\n");
            return 0;
        }
    }
    printf("%d\n", ans);

    return 0;
}
```
