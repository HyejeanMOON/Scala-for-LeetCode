You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

Example:
```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

Difficulty:Medium  
Total Accepted:46.5K  
Total Submissions:100.8K  
Related Topics:Linked List

### 解题思路
我们可以看到这道题的最高位在链表首位置，如果我们给链表翻转一下的话就跟之前的题目一样了，这里我们来看一些不修改链表顺序的方法。由于加法需要从最低位开始运算，而最低位在链表末尾，链表只能从前往后遍历，没法取到前面的元素，那怎么办呢？我们可以利用栈来保存所有的元素，然后利用栈的后进先出的特点就可以从后往前取数字了，我们首先遍历两个链表，将所有数字分别压入两个栈s1和s2中，我们建立一个值为0的res节点，然后开始循环，如果栈不为空，则将栈顶数字加入sum中，然后将res节点值赋为sum%10，然后新建一个进位节点head，赋值为sum/10，如果没有进位，那么就是0，然后我们head后面连上res，将res指向head，这样循环退出后，我们只要看res的值是否为0，为0返回res->next，不为0则返回res即可。
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
        var temp1 = l1
        var temp2 = l2
        var s1 = new scala.collection.mutable.Stack[Int]()
        var s2 = new scala.collection.mutable.Stack[Int]()
        while(temp1!=null){
            s1.push(temp1.x)
            temp1 = temp1.next
        }
        while(temp2!=null){
            s2.push(temp2.x)
            temp2 = temp2.next
        }
        var sum = 0
        var res = new ListNode(0)
        while(!s1.isEmpty || !s2.isEmpty){
            if(!s1.isEmpty){
                sum += s1.top
                s1.pop
            }
            if(!s2.isEmpty){
                sum += s2.top
                s2.pop
            }
            res.x = sum % 10
            var head = new ListNode(sum/10)
            head.next = res
            res = head
            sum /= 10
        }
        if(res.x==0) return res.next
        else return res
        res
    }
}
```