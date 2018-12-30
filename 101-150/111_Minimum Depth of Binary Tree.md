Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Difficulty:Easy  
Total Accepted:209.3K  
Total Submissions:623.8K  
Related Topics:Tree, Depth-first Search, Breadth-first Search

### 解题思路
用depth-first search来解决。实现的具体方法是递归。
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
    def minDepth(root: TreeNode): Int = {
        if(root == null) return 0
        if(root.left==null && root.right==null) return 1
        if(root.left ==null) return minDepth(root.right)+1
        else if(root.right==null) return minDepth(root.left)+1
        else return 1+scala.math.min(minDepth(root.left),minDepth(root.right))
        0
    }
}
```