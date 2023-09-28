```c++
int BFS(Node start, Node target) {
    queue<Node> q; 
    set<Node> visited;
    
    q.push(start); 
    visited.insert(start);// 访问标记应该在进队时标记
    int cnt = 0;

    while (!q.empty()) {
        int sz = q.size();// 一定要先取出来，不能在for循环直接用q.size()，因为for里面的操作会改变q.size()
        cnt++;
        for (int i = 0; i < sz; i++) {
            Node cur = q.front();
            // 不能把设置访问标记写在此处，如果写在此处，仍然会重复访问
            // 1 0
            // 0 .
            // 队列中是上面的两个0，cur分别为左边的0和下边的0，此时就会重复加入左下角的.
            q.pop();
            if (cur == target)
                return step;
            for (Node x : cur.adj()) {
                if (visited.count(x) == 0) {
                    q.push(x);
                    visited.insert(x);// 访问标记应该在进队时标记
                }
            }
        }
    }
    // 如果走到这里，说明在图中没有找到目标节点
}
```
