You need to find the largest value in each row of a binary tree.

Example:
```
Input: 

          1
         / \
        3   2
       / \   \  
      5   3   9 

Output: [1, 3, 9]
```

Difficulty:Medium  
Total Accepted:37.9K  
Total Submissions:68.2K  
Related Topics: Tree, Depth-first Search, Breadth-first Search

### 解题思路
用广度优先搜索的方式。使用queue作为数据结构来储存每一层的value。
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
    def largestValues(root: TreeNode): List[Int] = {
        if(root == null) return List()
        var que = new scala.collection.mutable.Queue[TreeNode]()
        var res:List[Int] = List()
        que = que :+ root
        while(!que.isEmpty){
            var len = que.length
            var mx = scala.Int.MinValue
            for(i <- 0 until len){
                var f = que.dequeue()
                mx = scala.math.max(mx,f.value)
                if(f.left!=null) que = que :+ f.left
                if(f.right!=null) que = que :+ f.right
            }
            res = res :+ mx
        }
        res
    }
}
```
