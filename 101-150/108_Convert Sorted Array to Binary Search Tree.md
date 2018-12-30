Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:
```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
 ```
 
 Difficulty:Easy  
Total Accepted:184.1K  
Total Submissions:406.1K  
Related Topics:Tree, DFS

### 解题思路
这道题是要将有序数组转为二叉搜索树，所谓二叉搜索树，是一种始终满足左<根<右的特性，如果将二叉搜索树按中序遍历的话，得到的就是一个有序数组了。那么反过来，我们可以得知，根节点应该是有序数组的中间点，从中间点分开为左右两个有序数组，在分别找出其中间点作为原中间点的左右两个子节点，这不就是是二分查找法的核心思想么。所以这道题考的就是二分查找法，
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
    def sortedArrayToBST(nums: Array[Int]): TreeNode = {
        return sortedArrayToBST(nums,0,nums.length-1)
    }
    def sortedArrayToBST(nums:Array[Int],left:Int,right:Int):TreeNode={
        if(left>right) return null
        var mid = (right+left)/2
        var cur = new TreeNode(nums(mid))
        cur.left = sortedArrayToBST(nums,left,mid-1)
        cur.right = sortedArrayToBST(nums,mid+1,right)
        cur
    }
}
```