# Trie字符串统计
```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class TrieNode{
public:
    int val;
    int cnt;
    vector<TrieNode*> children;
    TrieNode(int _cnt){
        val = 0;// 计数
        cnt = _cnt;
        for (int i = 0; i < cnt; ++i)
            children.push_back(nullptr);
    }
};

int find_node(TrieNode* &root, string key){
    TrieNode* p = root;
    for (int i = 0; i < key.size(); ++i) {
        int index = key[i]-'a';
        if (p->children[index] == nullptr)
            return 0;
        else
            p = p->children[index];
    }
    return p->val;
}

void insert_node(TrieNode* &root, string key){
    TrieNode* p = root;
    for (int i = 0; i < key.size(); ++i) {
        int index = key[i]-'a';
        if (p->children[index] == nullptr){
            p->children[index] = new TrieNode(root->cnt);
            p = p->children[index];
        }else{
            p = p->children[index];
        }
    }
    p->val++;
}

int main(){
    TrieNode* root = new TrieNode(26);
    int n;
    cin >> n; getchar();
    for (int i = 0; i < n; ++i) {
        char op;
        scanf("%c", &op); getchar();
        string str;
        cin >> str; getchar();
        if (op == 'I')
            insert_node(root, str);
        else if (op == 'Q')
            printf("%d\n", find_node(root, str));
    }

    return 0;
}
```
