Given a linked list, determine if it has a cycle in it.

Follow up:  
Can you solve it without using extra space?

Difficulty:Easy  
Total Accepted:259.4K  
Total Submissions:741.2K  
Related Topics:Linked List, Two Pointers

### 解题思路
这道题是快慢指针的经典应用。只需要设两个指针，一个每次走一步的慢指针和一个每次走两步的快指针，如果链表里有环的话，两个指针最终肯定会相遇。
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
    public boolean hasCycle(ListNode head) {
        ListNode temp = head;
        ListNode fast = temp;
        ListNode slow = temp;
        while(fast!=null && fast.next!=null){
            fast=fast.next.next;
            slow=slow.next;
            if(slow==fast) return true;
        }
        return false;
    }
}
```