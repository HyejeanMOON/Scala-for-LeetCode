Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.

Example 1:
```
Input: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 9

Output: True
```
Example 2:
```
Input: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 28

Output: False
```


### 解题思路
该问题的解题思路还是用递归的方法收集各个节点的value。把这些value收集到Seq（）中，最后用遍历的方式查找是否可以组成target的值。
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
    def findTarget(root: TreeNode, k: Int): Boolean = {
        if(root == null) return false
        var res:Seq[Int] = Seq()
        res = recordTree(root)
        //res.foreach(println)
        var leng = res.length
        for(i <- 0 until leng-1){
            for(j <- i+1 until leng){
                if(res(i) + res(j) == k){
                    //println(res(i) + " " + res(j))
                    return true
                }
            }
        }
        return false
        
    }
    def recordTree(tree:TreeNode):Seq[Int] = {
        var res:Seq[Int] = Seq()
        if(tree == null) return res
        res = res :+ tree.value
        res = res ++: recordTree(tree.left)
        res = res ++: recordTree(tree.right)
        res
    }
}
```
#### Java
```java

```