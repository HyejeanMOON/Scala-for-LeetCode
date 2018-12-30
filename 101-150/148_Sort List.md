Sort a linked list in O(n log n) time using constant space complexity.

Difficulty:Medium  
Total Accepted:130.9K  
Total Submissions:438.6K  
Related Topics:Linked List, Sort

### 解题思路
跟147_Insetion sort list的解法是一样的。
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
    def sortList(head: ListNode): ListNode = {
        if(head==null) return head
        var record = new scala.collection.mutable.ArrayBuffer[Int]()
        var temp = head
        while(temp!=null){
            record = record :+ temp.x
            temp = temp.next
        }
        for(i <- 0 until record.length-1){
            var j = i+1
            var flag = true
            while(j>=1 && flag){
                if(record(j-1)<=record(j)) flag = false
                if(flag){
                    var t = record(j-1)
                    record(j-1) = record(j)
                    record(j) = t
                    j-=1
                }        
            }
        }
        var l = new ListNode(record(0))
        var h = l
        for(i <- 1 until record.length){
            l.next = new ListNode(record(i))
            l = l.next
        }
        h
    }
}
```