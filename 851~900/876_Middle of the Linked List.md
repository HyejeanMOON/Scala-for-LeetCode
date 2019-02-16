Given a non-empty, singly linked list with head node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

 

Example 1:
```
Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.
Example 2:

Input: [1,2,3,4,5,6]
Output: Node 4 from this list (Serialization: [4,5,6])
Since the list has two middle nodes with values 3 and 4, we return the second one.
```

Note:

The number of nodes in the given list will be between 1 and 100.

Difficulty:Easy  
Total Accepted:6K  
Total Submissions:8.7K  
Related Topics:Linked List

### 解题思路
用fast,slow双指针。
#### Scala
```Scala
/**
 * Definition for singly-linked list.
 * class ListNode(var _x: Int = 0) {
 *   var next: ListNode = null
 *   var x: Int = _x
 * }
 */
object Solution {
    def middleNode(head: ListNode): ListNode = {
        var fast = head
        var slow = head
        while(fast.next!=null && fast.next.next!=null){
            slow = slow.next
            fast = fast.next.next
        }
        if(fast.next!=null) slow=slow.next
        slow
    }
}
```

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while(fast.next!=null && fast.next.next!=null){
            slow=slow.next;
            fast=fast.next.next;
        }
        if(fast.next!=null) slow=slow.next;
        return slow;
    }
}
```