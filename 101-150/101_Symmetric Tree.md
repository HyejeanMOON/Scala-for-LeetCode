Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following [1,2,2,null,3,null,3] is not:
```
    1
   / \
  2   2
   \   \
   3    3
```
Note:  
Bonus points if you could solve it both recursively and iteratively.

Difficulty:Easy  
Total Accepted:254.2K  
Total Submissions:626.5K  
Related Topics:Tree, BFS, DFS

### 解题思路
判断二叉树是否是平衡树，比如有两个节点n1, n2，我们需要比较n1的左子节点的值和n2的右子节点的值是否相等，同时还要比较n1的右子节点的值和n2的左子结点的值是否相等，以此类推比较完所有的左右两个节点。我们可以用递归和迭代两种方法来实现，写法不同，但是算法核心都一样。

这道题不太适合使用BFS。因为涉及到NULL节点的处理。很难出考虑出NULL节点的时候是要记录，还是要要跳过比较合理。所以遇到这种类型的题的时候一定要使用递归。

这道题可以考虑使用双queue进行对比。
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
    def isSymmetric(root: TreeNode): Boolean = {
        if(root==null) return true
        return isSame(root.left,root.right)
    }
    def isSame(l:TreeNode, r:TreeNode):Boolean={
        var ll = l
        var rr = r
        if(ll==null && rr==null) return true
        if((ll==null && rr!=null) || (ll!=null && rr==null) || (ll.value!=rr.value)) return false
        return isSame(ll.left,rr.right) && isSame(ll.right,rr.left)
    }
}
```

---
除了递归，还可用队列进行BFS搜索。

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
    def isSymmetric(root: TreeNode): Boolean = {
        if(root==null) return true
        else if(root.left == null && root.right==null) return true
        else if((root.left==null && root.right!=null) || (root.left!=null && root.right==null)) return false
        var que1 = new scala.collection.mutable.Queue[TreeNode]()
        var que2 = new scala.collection.mutable.Queue[TreeNode]()
        que1 += root.left
        que2 += root.right
        while(!que1.isEmpty && !que2.isEmpty){
            if(que1.length!=que2.length) return false
            var v1 = que1.dequeue
            var v2 = que2.dequeue
            if((v1==null && v2!=null) || (v1!=null && v2==null)) return false
            if(v1!=null){  //防止空指针
                if(v1.value!=v2.value) return false
                que1 += v1.left
                que1 += v1.right
                que2 += v2.right  //在这里跟v1的加入顺序正好颠倒，让v1和v2自动有了对称关系。
                que2 += v2.left 
            }
        }
        true
    }
}
```