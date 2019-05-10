>https://leetcode.com/problems/palindrome-linked-list/

**expression**

Given a singly linked list, determine if it is a palindrome.

**Example 1:**

    Input: 1->2
    Output: false
    Example 2:

**Example 2:**

    Input: 1->2->2->1
    Output: true

**Follow up:**
Could you do it in O(n) time and O(1) space?

**comprehension**

回文链表：：使用快慢指针来实现。使用快慢指针找中点的原理：：fast和slow两个指针，每次快指针走两步，慢指针走一步，等快指针走完时，慢指针的位置就是中点。需要用到栈，每次慢指针走一步，都把值存入栈中，等到达中点时，链表的前半段都存入栈中了，由于栈的后进先出的性质，就可以和后半段的链表按照回文对应的顺序比较了。

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
    bool isPalindrome(ListNode* head) {
        if(!head||!head->next)
            return true;
        ListNode *slow=head,*fast=head;
        stack<int> s;
        s.push(head->val);
        while(fast->next&&fast->next->next){
            slow=slow->next;
            fast=fast->next->next;
            s.push(slow->val);
        }
        //and now. what slow pointed is the middle of the list
        if(!fast->next)
            s.pop();
        while(slow->next){
            slow=slow->next;
            int tmp=s.top();
            s.pop();
            if(tmp!=slow->val)
                return false;
        }
        return true;
    }
};
```
