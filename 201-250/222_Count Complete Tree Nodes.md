Given a complete binary tree, count the number of nodes.

Note:

Definition of a complete binary tree from Wikipedia:
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

Example:
```
Input: 
    1
   / \
  2   3
 / \  /
4  5 6

Output: 6
```

Difficulty:Medium  
Total Accepted:81.8K  
Total Submissions:291.1K  
Related Topics:Binary Search, Tree

### 解题思路
这道题只要用BFS扫描一遍树的节点，计数就可以了。


-----------
这道题给定了一棵完全二叉树，让我们求其节点的个数。很多人分不清完全二叉树和满二叉树的区别，下面让我们来看看维基百科上对二者的定义：

完全二叉树 (Complete Binary Tree)：

A Complete Binary Tree （CBT) is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.

对于一颗二叉树，假设其深度为d（d>1）。除了第d层外，其它各层的节点数目均已达最大值，且第d层所有节点从左向右连续地紧密排列，这样的二叉树被称为完全二叉树；

换句话说，完全二叉树从根结点到倒数第二层满足完美二叉树，最后一层可以不完全填充，其叶子结点都靠左对齐。

完美二叉树 (Perfect Binary Tree)：

A Perfect Binary Tree(PBT) is a tree with all leaf nodes at the same depth. All internal nodes have degree 2.

二叉树的第i层至多拥有2^{i-1}个节点数；深度为k的二叉树至多总共有{\displaystyle 2^{\begin{aligned}k+1\end{aligned}}-1}个节点数，而总计拥有节点数匹配的，称为“满二叉树”；

完满二叉树 (Full Binary Tree):

A Full Binary Tree (FBT) is a tree in which every node other than the leaves has two children.

换句话说，所有非叶子结点的度都是2。（只要你有孩子，你就必然是有两个孩子。）


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
    def countNodes(root: TreeNode): Int = {
        var res = 0
        if(root==null) return res
        var out = new scala.collection.mutable.Stack[TreeNode]()
        out.push(root)
        while(!out.isEmpty){
            var len = out.length
            for(i <- 0 until len){
                var temp = out.pop
                res+=1
                if(temp.left!=null) out.push(temp.left)
                if(temp.right!=null) out.push(temp.right)
            }
        }
        res
    }
}
```