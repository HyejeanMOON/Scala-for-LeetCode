Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

Note: Do not modify the linked list.

Follow up:
Can you solve it without using extra space?

Difficulty:Medium  
Total Accepted:148.6K  
Total Submissions:487.5K  
Related Topics:Linked List, Two Pointers

### 解题思路
在链表的题中需要比较两个节点是否是一致的问题中，一定要用双指针，也就是一个fast，一个slow。  
该题中fast比slow快一倍，如果是循环链表的话，此时再相遇的位置就是链表中环的起始位置。
#### Scala
```scala
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while(fast!=null && fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow==fast) break;
        }
        if(fast==null || fast.next==null) return null;
        slow = head;
        while(slow!=fast){
            slow=slow.next;
            fast=fast.next;
        }
        return fast;
    }
}
```