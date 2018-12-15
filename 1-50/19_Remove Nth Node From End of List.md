Given a linked list, remove the n-th node from the end of list and return its head.

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:

Given n will always be valid.

Follow up:

Could you do this in one pass?

Difficulty:Medium  
Total Accepted:254.7K  
Total Submissions:751K  
Related Topics:Linked List, Two Pointers

### 解题思路
首先可以用最笨的方法，把链表的所有值都记录下来，然后去除指定的元素以后再重新构建链表。
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
    def removeNthFromEnd(head: ListNode, n: Int): ListNode = {
        var temp = head
        var r:Array[Int] = Array()
        while(temp!=null){
            r=r:+temp.x
            temp = temp.next
        }
        var t =  new ListNode(-1)
        var res = t
        for(i <- 0 until r.length){
            if(i!=r.length-n){
                t.next = new ListNode(r(i))
                t=t.next
            }
        }
        res.next
    }
}
```

---
如果想要满足follow up的话需要用到Two pointers。  
这道题让我们移除链表倒数第N个节点，限定n一定是有效的，即n不会大于链表中的元素总数。还有题目要求我们一次遍历解决问题，那么就得想些比较巧妙的方法了。比如我们首先要考虑的时，如何找到倒数第N个节点，由于只允许一次遍历，所以我们不能用一次完整的遍历来统计链表中元素的个数，而是遍历到对应位置就应该移除了。那么我们需要用两个指针来帮助我们解题，pre和cur指针。首先cur指针先向前走N步，如果此时cur指向空，说明N为链表的长度，则需要移除的为首元素，那么此时我们返回head->next即可，如果cur存在，我们再继续往下走，此时pre指针也跟着走，直到cur为最后一个元素时停止，此时pre指向要移除元素的前一个元素，我们再修改指针跳过需要移除的元素即可。


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
    def removeNthFromEnd(head: ListNode, n: Int): ListNode = {
        if(head.next==null) return null
        var temp = head
        var res = temp
        var pre = temp
        var cur = temp
        var count = 0
        for(i <- 0 until n){
            cur = cur.next
        }
        if(cur==null) return res.next
        while(cur.next!=null){
            pre=pre.next
            cur=cur.next
        }
        pre.next=pre.next.next
        res  
    }
}
```