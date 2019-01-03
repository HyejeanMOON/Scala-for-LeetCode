Given a singly linked list, determine if it is a palindrome.

Follow up:
Could you do it in O(n) time and O(1) space?

Difficulty:Easy  
Total Accepted:156.3K  
Total Submissions:467.1K  
Related Topics:Linked List, Two Pointers

### 解题思路
思路是，先把链表的数值存到数组中。然后用二分法查找是否是回文字符。
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
    def isPalindrome(head: ListNode): Boolean = {
        var temp = head
        if(head==null) return true
        var record:Array[Int] = Array()
        while(temp!=null){
            record = record :+ temp.x
            temp = temp.next
        }
        var left = 0
        var right = record.length-1
        while(left<right){
            if(record(left)!=record(right)) return false
            left+=1
            right-=1
        }
        true
    }
}
```

### 解题思路
我们使用快慢指针找中点的原理是fast和slow两个指针，每次快指针走两步，慢指针走一步，等快指针走完时，慢指针的位置就是中点。我们还需要用栈，每次慢指针走一步，都把值存入栈中，等到达中点时，链表的前半段都存入栈中了，由于栈的后进先出的性质，就可以和后半段链表按照回文对应的顺序比较了。
#### Scala
```scala
```

http://www.cnblogs.com/grandyang/p/4635425.html