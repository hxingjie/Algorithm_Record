```c++
int BFS(Node start, Node target) {
    queue<Node> q; 
    set<Node> visited;
    
    q.push(start); 
    visited.insert(start);
    int cnt = 0;

    while (!q.empty()) {
        int sz = q.size();// 一定要先取出来，不能在for循环直接用q.size()，因为for里面的操作会改变q.size()
        cnt++;
        for (int i = 0; i < sz; i++) {
            Node cur = q.front();
            q.pop();
            if (cur == target)
                return step;
            for (Node x : cur.adj()) {
                if (visited.count(x) == 0) {
                    q.push(x);
                    visited.insert(x);
                }
            }
        }
    }
    // 如果走到这里，说明在图中没有找到目标节点
}
```
