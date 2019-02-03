Find the sum of all left leaves in a given binary tree.

Example:
```
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```
Difficulty:Easy  
Total Accepted:82.4K  
Total Submissions:173.6K  
Related Topics : Tree

### 解题思路
该题的解题思路是用递归。然后判断的方法是如果左节点的左右子节点都没有的话就把value加上去。
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
    def sumOfLeftLeaves(root: TreeNode): Int = {
        if(root==null) return 0
        if(root.left!=null && root.left.left ==null && root.left.right==null){
            return root.left.value + sumOfLeftLeaves(root.right)
        }
        return sumOfLeftLeaves(root.left) + sumOfLeftLeaves(root.right)
    }
}
```