Given the root node of a binary search tree (BST) and a value. You need to find the node in the BST that the node's value equals the given value. Return the subtree rooted with that node. If such node doesn't exist, you should return NULL.

For example, 
```
Given the tree:
        4
       / \
      2   7
     / \
    1   3

And the value to search: 2
```
You should return this subtree:
```
      2     
     / \   
    1   3
```
In the example above, if we want to search the value 5, since there is no node with value 5, we should return NULL.

Note that an empty tree is represented by NULL, therefore you would see the expected output (serialized tree format) as [], not null.

Difficulty:Easy  
Total Accepted:1.4K  
Total Submissions:4.4K  
Related Topics :Tree

### 解题思路
用BFS搜索。
#### Scala
```Scala
/**
 * Definition for a binary tree node.
 * class TreeNode(var _value: Int) {
 *   var value: Int = _value
 *   var left: TreeNode = null
 *   var right: TreeNode = null
 * }
 */
object Solution {
    def searchBST(root: TreeNode, `val`: Int): TreeNode = {
        if(root==null) return root
        var que = new scala.collection.mutable.Queue[TreeNode]()
        que.enqueue(root)
        while(!que.isEmpty){
            var len = que.length
            for(i <- 0 until len){
                var tempNode = que.dequeue
                if(tempNode.value==`val`) return tempNode
                if(tempNode.left!=null) que.enqueue(tempNode.left)
                if(tempNode.right!=null) que.enqueue(tempNode.right)
            }
        }
        null
    }
}
```