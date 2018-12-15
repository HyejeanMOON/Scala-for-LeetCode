Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:
```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

Difficulty:Hard  
Total Accepted:226.6K  
Total Submissions:794.7K  
Related Topics: Linked List, Devide and Conquer, Heap

### 解题思路
这是比较笨的方法，时间复杂度也达到了O(nlogn)。 首先是把输入中的所有的链表的值都过去。然后进行排序。然后在重新构建链表。
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
    def mergeKLists(lists: Array[ListNode]): ListNode = {
        var record:List[Int] = List()
        for(list <- lists){
            var temp = list
            while(temp!=null){
                record = record:+temp.x
                temp = temp.next
            }
        }
        record = record.sorted
        var head = new ListNode(-1)
        var res = head
        for(i <- 0 until record.length){
            head.next = new ListNode(record(i))
            head = head.next
        }
        res.next
    }
}
```

### C++
```C++
class Solution {
public:
    ListNode *mergeKLists(vector<ListNode *> &lists) {
        if (lists.size() == 0) return NULL;
        int n = lists.size();
        while (n > 1) {
            int k = (n + 1) / 2;
            for (int i = 0; i < n / 2; ++i) {
                lists[i] = mergeTwoLists(lists[i], lists[i + k]);
            }
            n = k;
        }
        return lists[0];
    }
    
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
        ListNode *head = new ListNode(-1);
        ListNode *cur = head;
        while (l1 && l2) {
            if (l1->val < l2->val) {
                cur->next = l1;
                l1 = l1->next;
            } else {
                cur->next = l2;
                l2 = l2->next;
            }
            cur = cur->next;
        }
        if (l1) cur->next = l1;
        if (l2) cur->next = l2;
        return head->next;
    }
};
```
