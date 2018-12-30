Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

For example:

Given binary tree [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
return its depth = 3.


### 解题思路
使用深度优先搜索的方法返回左右节点中最深的深度数。  
铭记，关于树的题都是用递归来解决的。
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
    def maxDepth(root: TreeNode): Int = {
        if(root == null) return 0
        return 1 + scala.math.max(maxDepth(root.left),maxDepth(root.right))
    }
}
```