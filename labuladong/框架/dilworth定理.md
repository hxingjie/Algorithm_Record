```c++
//木棍加工

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Node{
public:
    int x,y;
};
bool cmp(const Node& lhs, const Node& rhs){
    if (lhs.x > rhs.x || (lhs.x == rhs.x && lhs.y > rhs.y)){
        return true;
    }else{
        return false;
    }
}
int main(){
    int n;
    cin >> n;

    vector<Node> nodes;
    for (int i = 0; i < n; ++i) {
        Node node;
        cin >> node.x >> node.y;
        nodes.push_back(node);
    }
    sort(nodes.begin(),nodes.end(),&cmp);
    vector<int> dp(n,1);
    int cnt = 0;
    for (int i = 1; i < n; ++i) {
        for (int j = i-1; j >= 0; --j) {
            if (nodes[i].y > nodes[j].y){
                dp[i] = max(dp[i],dp[j]+1);
            }
        }
        cnt = max(cnt,dp[i]);
    }
    // 最少不上升(num[i]>=num[i+1])子序列的个数 等于 最长上升(num[i]<num[i+1])子序列的长度
    cout << cnt << endl;

    return 0;
}
```

