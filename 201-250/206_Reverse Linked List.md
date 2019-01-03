Reverse a singly linked list.

Difficulty:Easy  
Total Accepted:343.3K  
Total Submissions:733.7K  
Related Topics:Linked List

### 解题思路
最笨的方法是把链表的所有value都获取了，然后reverse。最后自己在制作一个链表就好了。
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
    def reverseList(head: ListNode): ListNode = {
        if(head==null || head.next==null) return head
        var record:Array[Int] = Array()
        var hh= head
        while(hh!=null){
            record = record:+hh.x
            hh = hh.next
        }
        var r = record.reverse
        var h = new ListNode(r(0))
        var temp = h
        for(i <- 1 until r.length){
            h.next = new ListNode(r(i))
            h = h.next
        }
        temp
    }
}
```

