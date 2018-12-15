Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:
```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

Difficulty:Easy    
Total Accepted:336.8K  
Total Submissions:818.2K  
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
    def mergeTwoLists(l1: ListNode, l2: ListNode): ListNode = {
        var res = new ListNode(-1)
        var head = res
        var t1 = l1
        var t2 = l2
        while(t1!=null || t2!=null){
            if(t1!=null && t2!=null){
                if(t1.x>t2.x) {
                    res.next = new ListNode(t2.x)
                    t2 = t2.next
                }
                else if(t1.x<t2.x) {
                    res.next = new ListNode(t1.x)
                    t1 = t1.next
                }
                else if(t1.x==t2.x){
                    res.next = new ListNode(t1.x)
                    res = res.next
                    res.next = new ListNode(t2.x)
                    t1 = t1.next
                    t2 = t2.next
                }
                res = res.next
            }else if(t1!=null && t2==null){
                res.next = new ListNode(t1.x)
                res = res.next
                t1 = t1.next
            }else if(t1==null && t2!=null){
                res.next = new ListNode(t2.x)
                res = res.next
                t2 = t2.next
            }
        }
        head.next
    }
}
```

#### python
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        tmp = ListNode(0)
        res = tmp
        while l1!=None or l2!=None :
            if l1!=None and l2!=None :
                if l1.val>l2.val:
                    tmp.next=ListNode(l2.val)
                    tmp=tmp.next
                    l2=l2.next
                elif l2.val > l1.val :
                    tmp.next= ListNode(l1.val)
                    tmp=tmp.next
                    l1=l1.next
                elif l2.val==l1.val:
                    tmp.next=ListNode(l1.val)
                    tmp=tmp.next
                    tmp.next=ListNode(l2.val)
                    tmp=tmp.next
                    l1=l1.next
                    l2=l2.next
                
            
            elif l1!=None:
                tmp.next = ListNode(l1.val)
                tmp=tmp.next
                l1=l1.next
            elif l2!=None:
                tmp.next = ListNode(l2.val)
                tmp=tmp.next
                l2=l2.next
        
        return res.next
        
```