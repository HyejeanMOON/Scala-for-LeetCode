
Given a binary tree, return the postorder traversal of its nodes' values.

Example:
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
```
Follow up: Recursive solution is trivial, could you do it iteratively?

Difficulty:Hard  
Total Accepted:182K  
Total Submissions:426.3K  
Related Topics:Stack, Tree

### 解题思路
经典题目，求二叉树的后序遍历的非递归方法，跟前序，中序，层序一样都需要用到栈，后续的顺序是左-右-根，所以当一个节点值被取出来时，它的左右子节点要么不存在，要么已经被访问过了。我们先将根结点压入栈，然后定义一个辅助结点head，while循环的条件是栈不为空，在循环中，首先将栈顶结点t取出来，如果栈顶结点没有左右子结点，或者其左子结点是head，或者其右子结点是head的情况下。我们将栈顶结点值加入结果res中，并将栈顶元素移出栈，然后将head指向栈顶元素；否则的话就看如果右子结点不为空，将其加入栈，再看左子结点不为空的话，就加入栈，注意这里先右后左的顺序是因为栈的后入先出的特点，可以使得左子结点先被处理。下面来看为什么是这三个条件呢，首先如果栈顶元素如果没有左右子结点的话，说明其是叶结点，而且我们的入栈顺序保证了左子结点先被处理，所以此时的结点值就可以直接加入结果res了，然后移出栈，将head指向这个叶结点，这样的话head每次就是指向前一个处理过并且加入结果res的结点，那么如果栈顶结点的左子结点或者右子结点是head的话，说明其子结点已经加入结果res了，那么就可以处理当前结点了。
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
    def postorderTraversal(root: TreeNode): List[Int] = {
        var res:List[Int] = List()
        if(root==null) return res
        var sta = new scala.collection.mutable.Stack[TreeNode]()
        sta.push(root)
        var head = root
        while(!sta.isEmpty){
            var t = sta.top
            if(t.left==null && t.right==null || t.left==head || t.right==head){
                res = res :+ t.value
                sta.pop
                head = t
            }else{
                if(t.right!=null) sta.push(t.right)
                if(t.left!=null) sta.push(t.left)
            }
        }
        res
    }
}
```