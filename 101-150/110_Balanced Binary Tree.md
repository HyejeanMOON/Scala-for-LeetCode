Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example 1:
```
Given the following tree [3,9,20,null,null,15,7]:

    3
   / \
  9  20
    /  \
   15   7
Return true.
```
Example 2:
```
Given the following tree [1,2,2,3,3,null,null,4,4]:

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
Return false.
```

Difficulty:Easy  
Total Accepted:224.3K  
Total Submissions:582.8K  
Related Topics: Tree, DFS

### 解题思路
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
    def isBalanced(root: TreeNode): Boolean = {
        if(root==null) return true
        if(scala.math.abs(getDepth(root.left)-getDepth(root.right))>1) return false
        return isBalanced(root.left) && isBalanced(root.right)
        
    }
    def getDepth(tree:TreeNode):Int = {
        if(tree==null) return 0
        return 1+ scala.math.max(getDepth(tree.left),getDepth(tree.right))
    }
}
```