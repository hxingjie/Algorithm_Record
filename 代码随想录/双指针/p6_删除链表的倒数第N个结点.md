# 删除链表的倒数第N个结点

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

```c++
// 快慢指针
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode * headNode = new ListNode(-1,head);
        ListNode * slow = headNode, * fast = headNode;

        for (size_t i = 0; i < n; i++) fast = fast->next;
        
        while (fast->next != nullptr){
            slow = slow->next;
            fast = fast->next;
        }
        slow->next = slow->next->next;
        
        return headNode->next;
    }
};
```

