Given a binary tree, return the preorder traversal of its nodes' values.

Example:
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]
```
Follow up: Recursive solution is trivial, could you do it iteratively?

Difficulty:Medium  
Total Accepted:234.5K  
Total Submissions:497.2K  
Related Topics:Stack, Tree

### 解题思路
preorder的顺序是根->左->右。  
这里需要用到stack，  
把右节点先放入stack，因为这样右节点一直被压着，  
可以先读取左节点进而形成先遍历左边。
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
    def preorderTraversal(root: TreeNode): List[Int] = {
        var res:List[Int] = List()
        if(root==null) return res
        var stack = new scala.collection.mutable.Stack[TreeNode]()
        stack.push(root)
        while(!stack.isEmpty){
            var temp = stack.pop
            res = res :+ temp.value
            if(temp.right!=null) stack.push(temp.right)
            if(temp.left!=null) stack.push(temp.left)
        }
        res
    }
}
```


---

下面这种写法使用了一个辅助结点p，这种写法其实可以看作是一个模版，对应的还有中序和后序的模版写法，形式很统一，方便于记忆。辅助结点p初始化为根结点，while循环的条件是栈不为空或者辅助结点p不为空，在循环中首先判断如果辅助结点p存在，那么先将p加入栈中，然后将p的结点值加入结果res中，此时p指向其左子结点。否则如果p不存在的话，表明没有左子结点，我们取出栈顶结点，将p指向栈顶结点的右子结点。

### Scala
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
    def preorderTraversal(root: TreeNode): List[Int] = {
        var res:List[Int] = List()
        var stack = new scala.collection.mutable.Stack[TreeNode]()
        var p = root
        while(!stack.isEmpty || p!=null){
            if(p!=null){
                stack.push(p)
                res = res :+ p.value
                p = p.left
            }else{
                var t = stack.pop
                p = t.right
            }
        }
        res
    }
}
```