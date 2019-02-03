Given a binary search tree with non-negative values, find the minimum absolute difference between values of any two nodes.

Example:
```
Input:

   1
    \
     3
    /
   2

Output:
1

Explanation:
The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
```
Note:   
There are at least two nodes in this BST.

### 解题思路
简单且经典的题。首先遍历数上的所有值，并用Set记录。因为Set不会记录相同的值，可以减少执行时间。然后计算各个数之间差值并记录，最后返回差值中的最小值。
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
    def getMinimumDifference(root: TreeNode): Int = {
        var res:Set[Int] = Set()
        if(root == null) return 0
        res ++= helper(root)
        var resArray = res.toArray
        var leng = resArray.length
        var result:Set[Int] = Set()
        for(i <- 0 until leng-1){
            for(j <- i+1 until leng){
                result += scala.math.abs(resArray(i) - resArray(j))
            }
        }
        result.min
        
    }
    def helper(tree:TreeNode):Set[Int] ={
        var res:Set[Int] = Set()
        if(tree == null) return res
        else res += tree.value
        res ++= helper(tree.left)
        res ++= helper(tree.right)
        res
    }
}
```