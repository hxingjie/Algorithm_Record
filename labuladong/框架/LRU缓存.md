```c++
class LRUCache {
public:
    class Node{
    public:
        int key, val;
        Node * prev, * next;
    };
    Node * head, * rail;
    map<int,Node*> m;
    int capacity;
    int size;

    LRUCache(int capacity) {
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
        if (m.count(key) == 0)
            return -1;

        pop_Node(m[key]);
        push_back(m[key]->key,m[key]->val);
        return m[key]->val;
    }

    void push_back(int key, int value){
        Node *p = new Node;
        p->key = key;
        p->val = value;
        p->prev = rail->prev;
        p->next = rail;
        rail->prev->next = p;
        rail->prev = p;
        m[key] = p;
    }

    void pop_Node(Node* p){
        p->prev->next = p->next;
        p->next->prev = p->prev;
    }

    void put(int key, int value) {
        if (m.count(key) > 0){// 已经有，就更新value
            m[key]->val = value;// 更新结点值
            pop_Node(m[key]);
            push_back(m[key]->key, m[key]->val);
            return;
        }

        if (size == capacity){
            Node * p = head->next;
            pop_Node(p);
            m.erase(p->key);
            delete p;
            size--;
        }
        push_back(key,value);
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
