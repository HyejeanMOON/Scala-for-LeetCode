Invert a binary tree.
```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
to
```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
  
Difficulty:Easy  
Total Accepted:231.1K  
Total Submissions:432.3K  
Related Topics:Tree

### 解题思路
使用BFS来手机node的同时可以交换节点的位置。
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
    def invertTree(root: TreeNode): TreeNode = {
        var que = new scala.collection.mutable.Queue[TreeNode]()
        var tree = root
        if(tree==null) return tree
        que.enqueue(tree)
        while(!que.isEmpty){
            var cur = que.dequeue
            var temp = cur.left
            cur.left = cur.right
            cur.right = temp
            if(cur.left!=null) que.enqueue(cur.left)
            if(cur.right!=null) que.enqueue(cur.right)
        }
        tree
    }
}
```


---

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
    def invertTree(root: TreeNode): TreeNode = {
        if(root==null ) return root
        var temp = root.left
        root.left = invertTree(root.right)
        root.right = invertTree(temp)
        root
    }
}
```