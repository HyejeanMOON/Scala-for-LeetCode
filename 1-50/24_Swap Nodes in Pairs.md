Given a linked list, swap every two adjacent nodes and return its head.

Example:
```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```
Note:

Your algorithm should use only constant extra space.
You may not modify the values in the list's nodes, only nodes itself may be changed.

Difficulty:Medium   
Total Accepted:221.8K  
Total Submissions:557.7K  
Related Topics:Linked List

### 解题思路
只要捋清思路就好了。
#### Scala
```scala
/**
 * Definition for singly-linked list.
 * class ListNode(var _x: Int = 0) {
 *   var next: ListNode = null
 *   var x: Int = _x
 * }
 */
object Solution {
    def swapPairs(head: ListNode): ListNode = {
        var pre = new ListNode(-1)
        var res = pre
        pre.next = head
        while(pre.next!=null && pre.next.next!=null){
            var temp = pre.next.next
            pre.next.next = temp.next
            temp.next= pre.next
            pre.next=temp
            pre=temp.next          
        }
        res.next
    }
}
```