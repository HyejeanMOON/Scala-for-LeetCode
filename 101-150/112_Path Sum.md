Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:
```
Given the below binary tree and sum = 22,

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.
```

Difficulty:Easy  
Total Accepted:208.4K  
Total Submissions:598.4K  
Related Topics:Tree,  Depth-First-Search

### 解题思路
该题需要用深度优先搜索。返回递归。如果root为空则返回false，如果没有子节点，且正好达到叶，则返回true。
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
    def hasPathSum(root: TreeNode, sum: Int): Boolean = {
        if(root == null) return false
        var temp = sum-root.value
        if(temp == 0 && root.left==null && root.right == null) return true
        return hasPathSum(root.left,temp) || hasPathSum(root.right,temp)
        
    }
    
}
```