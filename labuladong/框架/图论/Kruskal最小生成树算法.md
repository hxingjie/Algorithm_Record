```c++
class Solution {
public:
    class UF{
    public:
        int cnt;
        vector<int> parent;
        UF(int n) : cnt(n){
            parent = vector<int>(n);
            for (int i = 0; i < n; ++i) {
                parent[i] = i;
            }
        }

        void union_node(int l, int r){
            int l_parent = find_parent(l);
            int r_parent = find_parent(r);

            if (l_parent == r_parent)
                return;

            parent[l_parent] = r_parent;
            cnt--;
        }

        int find_parent(int n){
            if (parent[n] != n){
                parent[n] = find_parent(parent[n]);
            }
            return parent[n];
        }

        bool isConnected(int l, int r){
            return find_parent(l) == find_parent(r);
        }

    };
    class cmp{
    public:
        bool operator () (const vector<int> &l, const vector<int> &r) const{
            if (l[2] < r[2])
                return true;
            else
                return false;
        }
    };
    int minCostConnectPoints(vector<vector<int>>& points) {
        vector<vector<int>> edges;
        for (int i = 0; i < points.size(); ++i) {
            for (int j = i+1; j < points.size(); ++j) {
                int x1 = points[i][0], y1 = points[i][1];
                int x2 = points[j][0], y2 = points[j][1];
                vector<int> edge{i, j, abs(x1-x2) + abs(y1-y2)};
                edges.push_back(edge);
            }
        }
        sort(edges.begin(), edges.end(), cmp());
        UF uf(points.size());
        
        int ans = 0;
        for (int i = 0; i < edges.size(); ++i) {
            if (!uf.isConnected(edges[i][0], edges[i][1])){
                ans += edges[i][2];
                uf.union_node(edges[i][0], edges[i][1]);
            }
        }
        return ans;
    }
};
```
