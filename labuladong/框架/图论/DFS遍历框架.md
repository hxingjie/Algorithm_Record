## 1.图问题

```c++
// 记录被遍历过的节点
vector<bool> visited;
// 记录从起点到当前节点的路径
vector<int> onPath;

/* 图遍历框架 */
void dfs(Graph graph, int idx) {
    if (visited[idx]) return;
    // 经过节点 s，标记为已遍历
    visited[idx] = true;
    // 做选择：标记节点 s 在路径上
    onPath.push_back(idx);
    for (int neighbor : graph.neighbors(idx)) {
        traverse(graph, neighbor);
    }
    // 撤销选择：节点 s 离开路径
    onPath.pop_back();
}
```



## 2.棋盘图问题

```c++
// 岛屿问题
void dfs(vector<vector<char>> &matrix, int row, int col){
    if (row < 0 || col < 0 || row >= n || col >= m) return;

    if (matrix[row][col] == '0') return;
    matrix[row][col] = '0';

    dfs(matrix,row-1,col);
    dfs(matrix,row+1,col);
    dfs(matrix,row,col-1);
    dfs(matrix,row,col+1);
}
```

```c++
// 寻路问题
void dfs(vector<vector<bool>> &map, int row, int col){
    if (row < 0 || col < 0 || row >= n || col >= m) return;
    if (map[row][col] == true) return;
    
    cnt++;
    map[row][col] = true;

    if (Arrive at the destination){
        // 完成题目目标   
        map[row][col] = false;
        cnt--;   
        return;
    }

    for (int i = 0; i < dx.size(); i++)
        dfs(map,row+dx[i],col+dy[i]);

    map[row][col] = false;
    cnt--;
}
```

