Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

Example:
```
Input: head = 1->4->3->2->5->2, x = 3
Output: 1->2->2->4->3->5
```

Difficulty:Medium  
Total Accepted:125.7K  
Total Submissions:371.3K  
Related Topics:Linked List, Two Pointers

### 解题思路
这道题要求我们划分链表，把所有小于给定值的节点都移到前面，大于该值的节点顺序不变，相当于一个局部排序的问题。那么可以想到的一种解法是首先找到第一个大于或等于给定值的节点，用题目中给的例子来说就是先找到4，然后再找小于3的值，每找到一个就将其取出置于4之前即可。
#### scala
```scala
/**
 * Definition for singly-linked list.
 * class ListNode(var _x: Int = 0) {
 *   var next: ListNode = null
 *   var x: Int = _x
 * }
 */
object Solution {
    def partition(head: ListNode, x: Int): ListNode = {
        var h = head
        var res = new ListNode(-1)
        res.next = h
        var pre = res
        var cur = h
        while(pre.next!=null && pre.next.x<x) pre=pre.next
        //println(pre.x)
        cur=pre
        while(cur.next!=null){
            if(cur.next.x<x){
                var temp = cur.next
                cur.next=temp.next
                temp.next=pre.next
                pre.next=temp
                pre=pre.next
            }
            else{
                cur=cur.next
            }
        }
        res.next
        
    }
}
```