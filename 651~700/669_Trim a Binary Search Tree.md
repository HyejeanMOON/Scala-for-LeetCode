
Given a binary search tree and the lowest and highest boundaries as L and R, trim the tree so that all its elements lies in [L, R] (R >= L). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

Example 1:
```
Input: 
    1
   / \
  0   2

  L = 1
  R = 2

Output: 
    1
      \
       2
```       
Example 2:
```
Input: 
    3
   / \
  0   4
   \
    2
   /
  1

  L = 1
  R = 3

Output: 
      3
     / 
   2   
  /
 1
```



### 解题思路
需要用递归的方式。首先判断root是否为空。如果是空，则直接返回null。  
然后再进行对root.value的判断，如果比L小，则从root的right开始重新判断，因为left比root.value小，肯定不符合要求。对R的比较也是同理。
然后是把root的left和right分别进行修剪。
#### Scala
```
/**
 * Definition for a binary tree node.
 * class TreeNode(var _value: Int) {
 *   var value: Int = _value
 *   var left: TreeNode = null
 *   var right: TreeNode = null
 * }
 */
object Solution {
    def trimBST(root: TreeNode, L: Int, R: Int): TreeNode = {
        if(root == null) return null
        if(root.value < L) return trimBST(root.right,L,R)
        if(root.value > R) return trimBST(root.left,L,R)
        root.left = trimBST(root.left,L,R)
        root.right = trimBST(root.right,L,R)
        root
    }
}
```