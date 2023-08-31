https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/description/

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (root == nullptr) return vector<vector<int>>();

        vector<vector<int>> ans;
        queue<TreeNode*> q;
        q.push(root);
        
        bool isLtoR = true;
        while (!q.empty()){
            int sz = q.size();

            vector<int> level;
            for (int i = 0; i < sz; ++i) {
                TreeNode* cur = q.front();
                q.pop();
                
                level.push_back(cur->val);
                
                if (cur->left != nullptr) q.push(cur->left);
                if (cur->right != nullptr) q.push(cur->right);
            }
            if (isLtoR)
                ans.push_back(level);
            else{
                reverse(level.begin(),level.end());
                ans.push_back(level);
            }
            isLtoR = !isLtoR; 
        }
        return ans;
    }
};
```
