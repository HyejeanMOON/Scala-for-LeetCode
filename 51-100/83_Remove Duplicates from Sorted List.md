Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,  
Given 1->1->2, return 1->2.  
Given 1->1->2->3->3, return 1->2->3.  

Difficulty:Easy  
Total Accepted:231.4K  
Total Submissions:575K  
Related Topics:Linked List

### 解题思路
设置两个链表，一个fast，一个是slow。fast比slow快一个。
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
    def deleteDuplicates(head: ListNode): ListNode = {
        if(head==null || head.next==null) return head
        var fast = head
        var slow = head
        var h = slow
        var record = new scala.collection.mutable.Stack[Int]()
        record.push(fast.x)
        fast = fast.next
        while(fast!=null){
            var temp = record.top
            if(fast.x != temp){
                record.push(fast.x)
                slow = slow.next
            }else{
                var t = slow.next.next
                slow.next = t
            }
            fast = fast.next
        }
        h
    }
}
```