# 环形链表II

给定一个链表的头节点  `head` ，返回链表开始入环的第一个节点。 *如果链表无环，则返回 `null`。*

[142. 环形链表 II - 力扣（LeetCode）](https://leetcode.cn/problems/linked-list-cycle-ii/description/)

```c++
// 快慢指针找环，如果找到了环，就让一个指针指向头结点，然后两个指针相同速度继续走，再次相遇的结点即为环入口结点
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode * headNode = new ListNode(-1,head);
        ListNode * slow = headNode, * fast = headNode;
        while (fast->next != nullptr && fast->next->next != nullptr)
        {
            fast = fast->next->next;
            slow = slow->next;
            if (slow == fast)// 相遇了
            {
                slow = headNode;
                while (slow != fast){
                    slow = slow->next;
                    fast = fast->next;
                }
                return slow;
            }  
        }
        return nullptr;
    }
};
```

