设有 N 堆石子排成一排，其编号为 1,2,3,…,N。

每堆石子有一定的质量，可以用一个整数来描述，现在要将这 N 堆石子合并成为一堆。

每次只能合并相邻的两堆，合并的代价为这两堆石子的质量之和，合并后与这两堆石子相邻的石子将和新堆相邻，合并时由于选择的顺序不同，合并的总代价也不相同。

例如有 4 堆石子分别为 1 3 5 2， 我们可以先合并 1、2 堆，代价为 4，得到 4 5 2， 又合并 1、2 堆，代价为 9，得到 9 2 ，再合并得到 11，总代价为 4+9+11=24；

如果第二步是先合并 2、3 堆，则代价为 7，得到 4 7，最后一次合并代价为 11，总代价为 4+7+11=22。

问题是：找出一种合理的方法，使总的代价最小，输出最小代价。

```c++
int main(){
    // dp[i][j]: merge stones[i] -> stones[j] 的最小代价
    // dp[i][j]
    //      = min( dp[i][i] + dp[i+1][j], dp[i][i+1] + dp[i+1][j], ...dp[i][j-1] + dp[j-1][j] ) + weights[i][j];
    int n;
    cin >> n;
    vector<int> stones(n+1);
    for (int i = 1; i <= n; ++i)
        scanf("%d", &stones[i]);

    vector<int> weights(n+1, 0);// 前缀和
    for (int i = 1; i <= n; ++i)
        weights[i] = weights[i-1] + stones[i];

    vector<vector<int>> dp(n+1, vector<int>(n+1, 0));// dp[1][n]

    for (int i = n; i >= 1; --i) {
        for (int j = i; j <= n; ++j) {
            if (i == j){
                dp[i][j] = 0;
            }else{
                int temp = INT_MAX;
                for (int k = i; k < j; ++k) {
                    temp = min(temp, dp[i][k] + dp[k+1][j] + weights[j]-weights[i-1]);
                }
                dp[i][j] = temp;
            }
        }
    }
    printf("%d\n", dp[1][n]);

    return 0;
}
```
