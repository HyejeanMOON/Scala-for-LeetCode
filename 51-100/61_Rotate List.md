Given a list, rotate the list to the right by k places, where k is non-negative.


Example:
```
Given 1->2->3->4->5->NULL and k = 2,

return 4->5->1->2->3->NULL.
```

### 解题思路
这道旋转链表的题和之前那道 Rotate Array 旋转数组 很类似，但是比那道要难一些，因为链表的值不能通过下表来访问，只能一个一个的走，我刚开始拿到这题首先想到的就是用快慢指针来解，快指针先走k步，然后两个指针一起走，当快指针走到末尾时，慢指针的下一个位置是新的顺序的头结点，这样就可以旋转链表了，自信满满的写完程序，放到OJ上跑，以为能一次通过，结果跪在了各种特殊情况，首先一个就是当原链表为空时，直接返回NULL，还有就是当k大于链表长度和k远远大于链表长度时该如何处理，我们需要首先遍历一遍原链表得到链表长度n，然后k对n取余，这样k肯定小于n，就可以用上面的算法了。
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
    def rotateRight(head: ListNode, k: Int): ListNode = {
        if(head == null) return null
        var temp = head; var count = 0
        while(temp != null){
            count+=1
            temp = temp.next
        }
        var t = k%count
        var fast = head; var slow = head
        for(i<- 0 until t){
            if(fast != null) fast = fast.next
        }
        if(fast==null) return head
        while(fast.next != null){
            fast = fast.next
            slow = slow.next
        }
        fast.next = head
        fast = slow.next
        slow.next = null
        fast
    }
}
```