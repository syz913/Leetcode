> 题目描述：给定一个有序链表，删除所有重复部分。

eg:

```java
Example 1:

Input: 1->1->2
Output: 1->2
Example 2:

Input: 1->1->2->3->3
Output: 1->2->3
```

> 思路描述：若next的值等于当前值，那么next就指向next->next，否则current移到next即可

```C++
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
    void deleteDplicates(ListNode* head){
        if(head == NULL){
            return;
        }
        if(head->next == NULL){
            return;
        }
        if(head->next->val == head->val){
            head->next = head->next->next;
            deleteDplicates(head);
        }else{
            deleteDplicates(head->next);
        }
    }
    ListNode* deleteDuplicates(ListNode* head) {
        deleteDplicates(head);
        return head;
    }
};
```

```C++
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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* current = head;
        if(current == NULL)
            return head;
        while(current->next != NULL){
            if(current->val == current->next->val){
                current->next = current->next->next;

            }else{
                current = current->next;
            }
        }
        return head;
    }
};
```

