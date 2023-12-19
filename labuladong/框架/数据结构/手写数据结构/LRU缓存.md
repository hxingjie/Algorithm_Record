## LRU缓存

请你设计并实现一个满足  LRU (最近最少使用) 缓存 约束的数据结构。
实现 LRUCache 类：
LRUCache(int capacity) 以 正整数 作为容量 capacity 初始化 LRU 缓存
int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
void put(int key, int value) 如果关键字 key 已经存在，则变更其数据值 value ；如果不存在，则向缓存中插入该组 key-value 。如果插入操作导致关键字数量超过 capacity ，则应该 逐出 最久未使用的关键字。
函数 get 和 put 必须以 O(1) 的平均时间复杂度运行。

https://leetcode.cn/problems/lru-cache/

```c++
class LRUCache {
public:
    class Node{
    public:
        int key, val;
        Node * prev, * next;
    };
    Node * head, * rail;// 链表实现记录使用次序
    map<int,Node*> m;// 哈希表：记录 key -> node(key,val)，实现O(1)取值
    int capacity;
    int size;

    LRUCache(int capacity) {// 初始化双向链表（有头尾结点）
        head = new Node;
        rail = new Node;
        head->prev = rail;
        head->next = rail;
        rail->prev = head;
        rail->next = head;
        this->capacity = capacity;
        size = 0;
    }

    int get(int key) {
        if (m.count(key) == 0)// key不存在
            return -1;

        pop_Node(m[key]);
        push_back(m[key]->key,m[key]->val);
        return m[key]->val;
    }

    void push_back(int key, int value){// 链表末尾插入结点
        Node *p = new Node;
        p->key = key;
        p->val = value;
        p->prev = rail->prev;
        p->next = rail;
        rail->prev->next = p;
        rail->prev = p;
        m[key] = p;
    }

    void pop_Node(Node* p){// 弹出结点
        p->prev->next = p->next;
        p->next->prev = p->prev;
    }

    void put(int key, int value) {
        if (m.count(key) > 0){// 已经存在与缓存中，就更新value
            m[key]->val = value;// 更新键值对，map中的结点和list中的结点是同一个，更新一个就行

            // 先弹出node，再插入node，更新使用次序
            pop_Node(m[key]);
            push_back(m[key]->key, m[key]->val);

            return;
        }

        if (size == capacity){
            Node * p = head->next;
            pop_Node(p);// 弹出结点
            m.erase(p->key);// 更新键值对
            delete p;
            size--;
        }
        push_back(key,value);// 插入新结点
        size++;
        
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
