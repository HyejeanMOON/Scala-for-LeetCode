Sort a linked list using insertion sort.

Difficulty:Medium  
Total Accepted:118.3K  
Total Submissions:349.4K  
Related Topics:Linked List, Sort

### 解题思路
该题的要求是我们用插入排序方法把链表排序。插入排序的时间复杂度是O(n2)，空间复杂度是O(1)。该题是用简单的思路，先把给定链表的value都获取并存入ArrayBuffer中，并且用插入排序的方法在数组中排序。然后为它在制作链表即可。

- *在scala中for不能用倒序，所以这个时候一定要用while来实现。*

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
    def insertionSortList(head: ListNode): ListNode = {
        if(head==null) return head
        var temp = new scala.collection.mutable.ArrayBuffer[Int]()
        var ht = head
        while(ht!=null){
            temp = temp :+ ht.x
            ht = ht.next
        }
        var flag = true
        for(i <- 0 until temp.length-1){
            flag = true
            var j = i+1
            while(j>0 && flag){
                if(temp(j-1)<=temp(j)) flag = false
                if(flag){
                    var t = temp(j-1)
                    temp(j-1) = temp(j)
                    temp(j) = t
                    j -= 1
                }
            }
        }
        var res = new ListNode(temp(0))
        var h = res
        for(i <- 1 until temp.length){
            println(temp(i))
            res.next = new ListNode(temp(i))
            res = res.next
        }
        h
    }
}
```