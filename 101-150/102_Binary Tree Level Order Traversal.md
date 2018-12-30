Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
```
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
```
return its level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
```
 
Difficulty:Medium   
Total Accepted:243K  
Total Submissions:565K  
Related Topics:Tree, BFS

### 解题思路
使用bfs把每一层的value记录就可以了。
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
    def levelOrder(root: TreeNode): List[List[Int]] = {
        var res:List[List[Int]] = List()
        if(root==null) return List()
        var que = new scala.collection.mutable.Queue[TreeNode]()
        que.enqueue(root)
        while(!que.isEmpty){
            var len = que.size
            var r:List[Int] = List()
            for(i <- 0 until len){
                var temp = que.dequeue
                r = r :+ temp.value
                if(temp.left!=null) que.enqueue(temp.left)
                if(temp.right!=null) que.enqueue(temp.right)
            }
            res = res :+ r
        }
        res
    }
}
```