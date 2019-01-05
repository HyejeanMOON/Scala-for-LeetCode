Given a binary tree, return all root-to-leaf paths.

Note: A leaf is a node with no children.

Example:
```
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```

Difficulty:Easy  
Total Accepted:167.2K  
Total Submissions:397.4K  
Related Topics:Tree, DFS

### 解题思路
用DFS就可以了，很简单。

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
    def binaryTreePaths(root: TreeNode): List[String] = {
        if(root==null) return List()
        var res:List[String] = List()
        var topNode = root.value
        res = dfs(root,"",res)
        res
    }
    def dfs(root:TreeNode, out:String, res:List[String]):List[String]={
        if(root==null) return res
        var tempres = res
        var tempout = out
        tempout += root.value
        if(root.left==null && root.right==null){
            tempres = tempres :+ tempout
        }
        tempres=dfs(root.left,tempout+"->",tempres)
        tempres=dfs(root.right,tempout+"->",tempres)
        tempres
        
        
    }
}
```