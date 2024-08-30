# LRU算法和LFU算法

## LRU算法
https://leetcode.cn/problems/lru-cache/
```c++
class LRUCache {
public:
    // 链表管理elem elem_i -> elem_i+1
    // 映射记录元素 key_i: elem_i
    // elem_i: key_i, val_i
    // put:
    //   1.新元素
    //     1.不需要淘汰, 头插法
    //     2.淘汰最末尾, 头插法
    //   2.旧元素
    //     1.找到元素, 头插法
    // get:
    //   1.存在cache, 找到元素, 头插法
    //   2.不存在cache, return -1
    struct Node{
        Node* prev;
        Node* next;
        int key, val;
        Node(Node* _prev, Node* _next, int _key, int _val)
            : prev(_prev), next(_next), key(_key), val(_val) {}
    };
    int iCapacity;
    int size;
    Node* head;
    Node* end;
    unordered_map<int, Node*> umKey2Node;
    LRUCache(int capacity)
        : iCapacity(capacity), size(0), head(nullptr), end(nullptr), umKey2Node(unordered_map<int, Node*>()) {
        head = new Node(nullptr, nullptr, -1, -1);
        end = new Node(nullptr, nullptr, -1, -1);
        head->next = end;
        end->prev = head;
        // ~LRUCache: delete head
    }
    
    void remove(Node* cur, bool del=false) {
        cur->prev->next = cur->next;
        cur->next->prev = cur->prev;
        size -= 1;

        if (del) delete cur;
    }

    void push_front(Node* cur) {
        cur->next = head->next;
        cur->prev = head;

        head->next = cur;
        cur->next->prev = cur;

        size += 1;
    }

    int get(int key) {
        if (umKey2Node.find(key) == umKey2Node.end())
            return -1;
        // 更新节点
        remove(umKey2Node[key]);
        push_front(umKey2Node[key]);
        return umKey2Node[key]->val;
    }

    void put(int key, int value) {
        if (umKey2Node.find(key) != umKey2Node.end()) { // 找到元素，头插法
            Node* cur = umKey2Node[key];
            cur->val = value; // update value
            // 更新节点
            remove(cur);
            push_front(cur);
            return;
        }

        // 加入新元素
        Node* cur = new Node(nullptr, nullptr, key, value);      
        if (size < iCapacity) { // 不需要淘汰 直接头插法
            umKey2Node[key] = cur;
            push_front(cur);
        } else { // 淘汰最末尾，头插法
            umKey2Node.erase(end->prev->key);
            remove(end->prev, true); // del node

            umKey2Node[key] = cur;
            push_front(cur);
        }
    }
};
```

