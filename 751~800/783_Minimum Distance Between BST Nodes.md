Given a Binary Search Tree (BST) with the root node root, return the minimum difference between the values of any two different nodes in the tree.

Example :
```
Input: root = [4,2,6,1,3,null,null]
Output: 1
Explanation:
Note that root is a TreeNode object, not an array.

The given tree [4,2,6,1,3,null,null] is represented by the following diagram:

          4
        /   \
      2      6
     / \    
    1   3  

while the minimum difference in this tree is 1, it occurs between node 1 and node 2, also between node 3 and node 2.
```

### 解题思路
思路其实很简单。首先遍历树上的所有节点的值，并记录在Set中。然后再次遍历这些值，并记录它们之间的差值。最后返回这些差值中的最小值。
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
    def minDiffInBST(root: TreeNode): Int = {
        if(root == null) return 0
        var res:Set[Int] = Set()
        res += root.value
        res ++= helper(root)
        res.foreach(println)
        var resArray = res.toArray
        var leng = resArray.length
        var collect:Set[Int] = Set()
        for(i <- 0 until leng-1){
            for(j <- i+1 until leng){
                //println(resArray(j))
                collect += scala.math.abs(resArray(i) - resArray(j))
            }
        }
        //collect.foreach(println)
        collect.min
        
    }
    def helper(tree:TreeNode):Set[Int]={
        var res:Set[Int] = Set()
        if(tree == null) return res
        res += tree.value
        res ++= helper(tree.left)
        res ++= helper(tree.right)
        res
    }
}
```