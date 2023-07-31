## 打家劫舍III

小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为 `root` 。

除了 `root` 之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果 **两个直接相连的房子在同一天晚上被打劫** ，房屋将自动报警。

给定二叉树的 `root` 。返回 ***在不触动警报的情况下** ，小偷能够盗取的最高金额* 。

[337. 打家劫舍 III - 力扣（LeetCode）](https://leetcode.cn/problems/house-robber-iii/description/)

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    map<pair<TreeNode*, bool>, int> mem;
    int dp(TreeNode* root, bool stolen){
        if (root == nullptr) return 0;
        pair<TreeNode*, bool> p(root, stolen);
        if (mem.count(p) == 0){
            if (stolen){// 父结点抢了
                mem[p] = dp(root->left,false)
                        + dp(root->right,false);
            }else{
                mem[p] = max(
                    dp(root->left, true) + dp(root->right,true) + root->val,
                    dp(root->left, false) + dp(root->right, false)
                    );
            }
        }
        return mem[p];

    }
    int rob(TreeNode* root) {
        return dp(root, false);
    }
};
```

```c#
public class Solution
{
    public Dictionary<KeyValuePair<TreeNode, bool>, int> dict = new Dictionary<KeyValuePair<TreeNode, bool>, int>();
    public int dp(TreeNode root, bool stolen)
    {
        if (root == null) return 0;
            
        KeyValuePair<TreeNode, bool> kvPair = new KeyValuePair<TreeNode, bool>(root, stolen);
        if (!dict.ContainsKey(kvPair))
        {
            if (stolen)// 没得选，不能偷
            {
                dict.Add(kvPair,dp(root.left, false) + dp(root.right, false));
            }
            else// 有得选，选择偷或不偷
            {
                dict.Add(kvPair,Math.Max(
                    dp(root.left, false) + dp(root.right, false),
                    dp(root.left, true) + dp(root.right, true) + root.val
                )); 
            }
        }

        return dict[kvPair];

    }
    public int Rob(TreeNode root)
    {
        return dp(root, false);
    }
}
```

