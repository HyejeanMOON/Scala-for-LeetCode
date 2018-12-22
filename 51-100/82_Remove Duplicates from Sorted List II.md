Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

Example 1:
```
Input: 1->2->3->3->4->4->5
Output: 1->2->5
```
Example 2:
```
Input: 1->1->1->2->3
Output: 2->3
```

Difficulty:Medium  
Total Accepted:134.1K  
Total Submissions:446.7K  
Related Topics:Linked List

### 解题思路
用最笨的方法。遍历链表用哈希表来记录数字出现的次数。然后重新建立ListNode。
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
        var record = new scala.collection.mutable.ArrayBuffer[Int]()
        var tempHead = head
        var rm:Map[Int,Int] = Map()
        while(tempHead != null){
            record = record :+ tempHead.x
            var temp = rm.getOrElse(tempHead.x,0)
            temp += 1
            rm += (tempHead.x -> temp)
            tempHead = tempHead.next
        }
        var h = new ListNode(-1)
        var res = h
        for(r <- record){
            if(rm.getOrElse(r,0)==1){
                h.next = new ListNode(r)
                h = h.next
            }
        }
        res.next
        
    }
}
```