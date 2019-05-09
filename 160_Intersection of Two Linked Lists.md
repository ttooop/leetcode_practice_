>https://leetcode.com/problems/intersection-of-two-linked-lists/

**expression:**

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

begin to intersect at node c1.

**example:**

    Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
    Output: Reference of the node with value = 8
    Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.

**Notes:**

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.

**comprehension**

给定两个链表，找到一个位置将两个位置链接：：：连接点之后的链表值是相同的

可以用环的思想来做，让两条链表分别从各自的开头开始向后遍历，当其中一条遍历到末尾时，跳过另一条链表的开头继续遍历，两个指针最后会相等，而且只有两种情况，一种情况在交点处相遇，另一种情况在各自的末尾的空结点处相等。为什么会相等呢？因为两个指针走过的路程相同，是两个链表的长度之和，所以一定会相等。

AMAZING!!!

```
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(!headA||!headB)
            return NULL;
        ListNode *a=headA,*b=headB;
        while(a!=b){
            a=a?a->next:headB;
            b=b?b->next:headA;
        }
        return a;
    }
};
```
