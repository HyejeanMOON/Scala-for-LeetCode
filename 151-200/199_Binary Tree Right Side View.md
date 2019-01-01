Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Example:
```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

Difficulty:Medium  
Total Accepted:116.4K  
Total Submissions:267.8K  
Related Topics:Tree, DFS, BFS

### 解题思路
用BFS，然后把每层的最后一个节点的值记录就可以了。
#### Scala
```scala
/**
 * Definition for a binary tree node.
 * class TreeNode(var _value: Int) {
 *   var value: Int = _value
 *   var left: TreeNode = null
 *   var right: TreeNode = null
 * }
 */
object Solution {
    def rightSideView(root: TreeNode): List[Int] = {
        if(root==null) return List()
        var res:List[Int] = List()
        var que = new scala.collection.mutable.Queue[TreeNode]()
        que.enqueue(root)
        while(!que.isEmpty){
            var len = que.length
            for(i <- 0 until len){
                var temp = que.dequeue
                //println(temp.value)
                if(i==len-1){
                    res=res:+temp.value
                }
                if(temp.left!=null) que.enqueue(temp.left)
                if(temp.right!=null) que.enqueue(temp.right)
            }
        }
        res
    }
    
}
```
