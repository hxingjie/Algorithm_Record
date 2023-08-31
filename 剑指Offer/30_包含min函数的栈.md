https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/description/

**思路:** 使用两个栈，一个记录数据，一个记录入栈时栈的最小值
```c++
class MinStack {
public:
    /** initialize your data structure here. */
    stack<int> s;
    stack<int> record;
    MinStack() {

    }
    
    void push(int x) {
        if (s.size() == 0){
            s.push(x);
            record.push(x);
        }
        else{
            if (x < record.top()){
                s.push(x);
                record.push(x);
            }else{
                s.push(x);
                record.push(record.top());
            }
        }
    }
    
    void pop() {
        s.pop();
        record.pop();
    }
    
    int top() {
        return s.top();
    }
    
    int min() {
        return record.top();
    }
};
```
