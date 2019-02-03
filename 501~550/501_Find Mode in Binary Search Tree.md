Given a binary search tree (BST) with duplicates, find all the mode(s) (the most frequently occurred element) in the given BST.

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than or equal to the node's key.
The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
Both the left and right subtrees must also be binary search trees.
 

For example:
```
Given BST [1,null,2,2],

   1
    \
     2
    /
   2
 

return [2].
```
Note: If a tree has more than one mode, you can return them in any order.

Follow up: Could you do that without using any extra space? (Assume that the implicit stack space incurred due to recursion does not count).

Difficulty:Easy  
Total Accepted:38.4K  
Total Submissions:101.6K  
Related Topics:Tree

### 解题思路
首先用BFS来记录node出现的次数。然后进行对比，把最大的value的node放入res中。
#### Scala
```Scala
/**
 * Definition for a binary tree node.
 * class TreeNode(var _value: Int) {
 *   var value: Int = _value
 *   var left: TreeNode = null
 *   var right: TreeNode = null
 * }
 */
object Solution {
    def findMode(root: TreeNode): Array[Int] = {
        var res:Array[Int] = Array()
        var que = new scala.collection.mutable.Queue[TreeNode]()
        if(root==null) return Array()
        var record:Map[Int,Int] = Map()
        que.enqueue(root)
        while(!que.isEmpty){
            var len = que.length
            for(i <- 0 until len){
                var temp = que.dequeue
                var t = record.getOrElse(temp.value,0)
                t+=1
                record+=(temp.value -> t)
                if(temp.left!=null)  que.enqueue(temp.left)
                if(temp.right!=null)  que.enqueue(temp.right)
            }
        }
        var key = record.keySet
        for(k <- key){
            var times = record.getOrElse(k,0)
            if(res.isEmpty) res=res:+k
            else{
                var first = res(0)
                if(times>record.getOrElse(first,0)){
                    res=Array()
                    res=res:+k
                }else if(times==record.getOrElse(first,0)) res=res:+k
                
            }           
        }
        res
    }
}
```