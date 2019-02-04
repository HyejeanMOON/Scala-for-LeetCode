Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.
Example 1:
```
Input:
    3
   / \
  9  20
    /  \
   15   7
Output: [3, 14.5, 11]
Explanation:
The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
```
Note:  
The range of node's value is in the range of 32-bit signed integer.


### 解题思路

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
    def averageOfLevels(root: TreeNode): Array[Double] = {
        var result:Array[Double] = Array()
        var r:Array[TreeNode] = Array(root)
        while(!r.isEmpty){
            var leng = r.length
            var sum:Double = 0
            var temp:Array[TreeNode] = Array()
            for(i <- 0 until leng){
                var cur = r(i)
                sum += cur.value
                if(cur.left != null) temp = temp :+ cur.left
                if(cur.right != null) temp = temp :+ cur.right
            }
            r = temp
            result = result :+ sum/leng
        }
        
        result
        
    }
    
}
```