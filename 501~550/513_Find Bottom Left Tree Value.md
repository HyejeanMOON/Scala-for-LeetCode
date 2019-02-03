Given a binary tree, find the leftmost value in the last row of the tree.

Example 1:
```
Input:

    2
   / \
  1   3

Output:
1
```
Example 2: 
```
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```
Note:  
You may assume the tree (i.e., the given root node) is not NULL.

Difficulty:Medium  
Total Accepted:42.9K  
Total Submissions:76.5K  
Related Topics: Tree, BFS, DFS

### 解题思路
这道题是一道很典型的BFS的题。遍历每一层，然后在最后一层的时候把记录每层value的数组中的第一个返回就可以了。
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
    def findBottomLeftValue(root: TreeNode): Int = {
        var bd = new scala.collection.mutable.Queue[TreeNode]()
        var record:Array[TreeNode] = Array()
        bd += root
        while(!bd.isEmpty){
            var len = bd.size
            record = Array()
            for(i <- 0 until len){
                var temp = bd.dequeue
                if(temp.left!=null) bd += temp.left
                if(temp.right!=null) bd += temp.right
                println(temp.value)
                record = record:+temp
            } 
        }
        var t = record(0).value
        t
    }
}
```
