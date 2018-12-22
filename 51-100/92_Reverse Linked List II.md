Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.

Example:
```
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

Difficulty:Medium  
Total Accepted:138.5K  
Total Submissions:440.2K  
Related Topics:Linked List

### 解题思路
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
    def reverseBetween(head: ListNode, m: Int, n: Int): ListNode = {
        var dummy = new ListNode(-1)
        dummy.next = head
        var cur = dummy
        var pre = new ListNode(-1)
        var front = new ListNode(-1)
        var last = new ListNode(-1)
        for(i <- 1 to m-1) cur = cur.next
        pre = cur
        last = cur.next
        for(i <- m to n){
            cur = pre.next
            pre.next = cur.next
            cur.next = front
            front = cur
        }
        cur = pre.next
        pre.next = front
        last.next = cur
        dummy.next
    }
}
```
---

可以用最笨的方法。把链表的value都获取了，然后把指定的那一段进行reverse。然后重新制作链表就可以了。
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
    def reverseBetween(head: ListNode, m: Int, n: Int): ListNode = {
        var record = new scala.collection.mutable.ArrayBuffer[Int]()
        var temp = head
        while(temp!=null){
            record = record :+ temp.x
            temp = temp.next
        }
        var t:Array[Int] = Array()
        for(i <- 0 until record.length){
            if((i+1)>=m && (i+1)<=n) t = t :+ record(i)
        }
        t = t.reverse
        var h = new ListNode(-1)
        var res = h
        for(i <- 0 until record.length){
            if((i+1)>=m && (i+1)<=n){
                h.next = new ListNode(t(i+1-m))
                h = h.next
            }else{
                h.next = new ListNode(record(i))
                h = h.next
            }
        }
        res.next
    }
}
```