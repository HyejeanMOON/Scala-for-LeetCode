You need to construct a string consists of parenthesis and integers from a binary tree with the preorder traversing way.
The null node needs to be represented by empty parenthesis pair "()". And you need to omit all the empty parenthesis pairs that don't affect the one-to-one mapping relationship between the string and the original binary tree.
Example 1:
```
Input: Binary tree: [1,2,3,4]
       1
     /   \
    2     3
   /    
  4     

Output: "1(2(4))(3)"

Explanation: Originallay it needs to be "1(2(4)())(3()())", 
but you need to omit all the unnecessary empty parenthesis pairs. 
And it will be "1(2(4))(3)".
```
Example 2:
```
Input: Binary tree: [1,2,3,null,4]
       1
     /   \
    2     3
     \  
      4 

Output: "1(2()(4))(3)"

Explanation: Almost the same as the first example, 
except we can't omit the first parenthesis pair to break the one-to-one mapping relationship between the input and the output.
```

Difficulty:Easy  
Total Accepted:37.8K  
Total Submissions:75.6K  
Related Topics:String,  Tree

### 解题思路
#### Scala
```scala
**
 * Definition for a binary tree node.
 * class TreeNode(var _value: Int) {
 *   var value: Int = _value
 *   var left: TreeNode = null
 *   var right: TreeNode = null
 * }
 */
object Solution {
    def tree2str(t: TreeNode): String = {
        var res = ""
        if(t==null) return res
        res = dfs(t,res)
        var len = res.length
        return res.substring(1,len-1)
        
    }
    def dfs(t:TreeNode,res:String):String={
        var tempr = res
        if(t==null) return tempr
        tempr = tempr+"(" + t.value.toString
        if(t.left==null && t.right!=null){
            tempr = tempr+"()"
        }
        
        tempr=dfs(t.left,tempr)
        tempr=dfs(t.right,tempr)
        tempr = tempr + ")"
        tempr
    }
}
```
