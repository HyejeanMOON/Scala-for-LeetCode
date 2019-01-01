Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:
```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.
```

Notes:

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.


Difficulty:Easy  
Total Accepted:202.8K  
Total Submissions:659.1K  
Related Topics:Linked List


### 解题思路
我还以为以后在不能免费做OJ的题了呢，想不到OJ又放出了不需要买书就能做的题，业界良心啊，哈哈^_^。这道求两个链表的交点题要求执行时间为O(n)，则不能利用类似冒泡法原理去暴力查找相同点，事实证明如果链表很长的话，那样的方法效率很低。我也想到会不会是像之前删除重复元素的题一样需要用两个指针来遍历，可是想了好久也没想出来怎么弄。无奈上网搜大神们的解法，发觉其实解法很简单，因为如果两个链长度相同的话，那么对应的一个个比下去就能找到，所以只需要把长链表变短即可。具体算法为：分别遍历两个链表，得到分别对应的长度。然后求长度的差值，把较长的那个链表向后移动这个差值的个数，然后一一比较即可。
#### Java
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA==null || headB==null) return null;
        int lenA = getLen(headA);
        int lenB = getLen(headB);
        if(lenA>lenB){
            for(int i=0; i<lenA-lenB; i++) headA=headA.next;
        }else{
            for(int i=0; i<lenB-lenA; i++) headB=headB.next;
        }
        while(headA!=null && headB!=null && headA!=headB){
            headA=headA.next;
            headB=headB.next;
        }
        return (headA!=null && headB!=null) ? headA:null;
    }
    public int getLen(ListNode head){
        int len = 0;
        while(head!=null){
            head=head.next;
            len++;
        }
        return len;
    }
}
```


---

这道题还有一种特别巧妙的方法，虽然题目中强调了链表中不存在环，但是我们可以用环的思想来做，我们让两条链表分别从各自的开头开始往后遍历，当其中一条遍历到末尾时，我们跳到另一个条链表的开头继续遍历。两个指针最终会相等，而且只有两种情况，一种情况是在交点处相遇，另一种情况是在各自的末尾的空节点处相等。为什么一定会相等呢，因为两个指针走过的路程相同，是两个链表的长度之和，所以一定会相等。这个思路真的很巧妙，而且更重要的是代码写起来特别的简洁。

#### Java
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA==null || headB==null) return null;
        ListNode a = headA;
        ListNode b = headB;
        while(a!=b){
            a = (a!=null) ? a.next:headB;
            b = (b!=null) ? b.next:headA;
        }
        return a;
    }
}
```