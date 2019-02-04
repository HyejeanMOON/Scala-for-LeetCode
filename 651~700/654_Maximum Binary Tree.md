Given an integer array with no duplicates. A maximum tree building on this array is defined as follow:

The root is the maximum number in the array.
The left subtree is the maximum tree constructed from left part subarray divided by the maximum number.
The right subtree is the maximum tree constructed from right part subarray divided by the maximum number.
Construct the maximum tree by the given array and output the root node of this tree.

Example 1:
```
Input: [3,2,1,6,0,5]
Output: return the tree root node representing the following tree:

      6
    /   \
   3     5
    \    / 
     2  0   
       \
        1
```        
Note:
The size of the given array will be in the range [1,1000].

Difficulty:Medium  
Total Accepted:27.6K  
Total Submissions:39.6K  

Related Topics : Tree

### 解题思路
这道题给了我们一个数组，让我们创建一个最大二叉树，创建规则是数组中的最大值为根结点，然后分隔出的左右部分再分别创建最大二叉树。那么明眼人一看就知道这是分治法啊，果断上递归啊。首先就是要先找出数组中的最大值，由于数组是无序的，所以没啥好的办法，就直接遍历吧，找到了最大值，就创建一个结点，然后将左右两个子数组提取出来，分别调用递归函数并将结果连到该结点上，最后将结点返回即可。
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
    def constructMaximumBinaryTree(nums: Array[Int]): TreeNode = {
        if(nums.isEmpty) return null
        var mx = scala.Int.MinValue
        var mx_index = 0
        for(n <- 0 until nums.length){
            if(nums(n) > mx){
                mx = nums(n)
                mx_index = n
            }
        }
    var tree = new TreeNode(mx)
    var left = constructMaximumBinaryTree(nums.slice(0,mx_index))
    var right = constructMaximumBinaryTree(nums.slice(mx_index+1,nums.length))
    tree.left = left
    tree.right = right
    tree
    }
}
```