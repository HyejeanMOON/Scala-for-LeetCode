Remove all elements from a linked list of integers that have value val.

Example:
```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```
Credits:  
Special thanks to @mithmatt for adding this problem and creating all test cases.

Difficulty:Easy  
Total Accepted:155.1K  
Total Submissions:461.7K  
Related Topics:Linked List

### 解题思路
一直以next作为判断基准。  
但是注意的是如果是删掉了一个node的话是不用移到next的。如果移动的话反而之后一个节点被跳过了。
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
    def removeElements(head: ListNode, `val`: Int): ListNode = {
        var temp = new ListNode(-1)
        temp.next = head
        var res = temp
        var flag = true
        while(temp.next!=null && flag){
            if(temp.next.x==`val`){
                if(temp.next.next!=null){
                    temp.next=temp.next.next
                }else{
                    temp.next=null
                    flag = false
                }
            }else{
                temp = temp.next
            }
            
        }
        res.next
    }
}
```