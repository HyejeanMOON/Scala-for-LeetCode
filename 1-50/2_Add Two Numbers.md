You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

### 解题思路
这道并不是什么难题，算法很简单，链表的数据类型也不难。就是建立一个新链表，然后把输入的两个链表从头往后撸，每两个相加，添加一个新节点到新链表后面，就是要处理下进位问题。还有就是最高位的进位问题要最后特殊处理一下。
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
    def addTwoNumbers(l1: ListNode, l2: ListNode): ListNode = {
        var res = new ListNode(-1)
        //设置res的原因在于，让返回从cur的头开始。
        var cur = res
        var carry = 0
        var temp1 = l1
        var temp2 = l2
        while(temp1 != null || temp2 != null){
            var d1 = 0
            var d2 = 0
            if(temp1==null) d1 = 0
            else d1 = temp1.x
            if(temp2==null) d2 = 0
            else d2 = temp2.x
            var sum = d1 + d2 + carry
            carry = sum / 10
            cur.next = new ListNode(sum%10)
            cur = cur.next
            if(temp1 != null) temp1 = temp1.next
            if(temp2 != null) temp2 = temp2.next
        }
        if(carry == 1){
            cur.next = new ListNode(1)
        }
        return res.next
    }
}
```

#### Java
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode res = new ListNode(0);
        ListNode cur = res;
        int carry = 0;
        while(l1!=null || l2!=null){
            int d1=l1==null ? 0:l1.val;
            int d2=l2==null ? 0:l2.val;
            int sum = d1+d2+carry;
            carry = sum/10;
            cur.next = new ListNode(sum%10);
            cur = cur.next;
            if(l1!=null) l1 = l1.next;
            if(l2!=null) l2 = l2.next;
        }
        if(carry == 1){
            cur.next = new ListNode(1);
            //cur = cur.next;
        }
        return res.next;
        
    }
}
```