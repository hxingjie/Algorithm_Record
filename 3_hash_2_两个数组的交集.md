```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode * headNode = new ListNode(-1,head);

        ListNode * fast = headNode;
        ListNode * slow = headNode;

        while (fast != nullptr && fast->next != nullptr){
            fast = fast->next->next;
            slow = slow->next;

            if (fast == slow){
                ListNode * p1 = headNode;
                ListNode * p2 = fast;

                while (p1 != p2){
                    p1 = p1->next;
                    p2 = p2->next;
                }
                return p1;
            }
        }
        return nullptr;

    }
};
```

