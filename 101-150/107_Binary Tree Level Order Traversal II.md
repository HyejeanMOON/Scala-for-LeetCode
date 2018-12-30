Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
```
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
]
```

Difficulty:Easy  
Total Accepted:166.4K  
Total Submissions:391.5K  
Related Topics: Tree, BFS

### 解题思路
该题用bfs，把收集到的各层的数进行reverse就可以了。  
切记，bfs是用queue。  
如果涉及到前序遍历等的时候是用stack。

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
    def levelOrderBottom(root: TreeNode): List[List[Int]] = {
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
        res = res.reverse
        res
    }
}
```