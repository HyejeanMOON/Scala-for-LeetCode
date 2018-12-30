
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
```
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:
```
[
  [3],
  [20,9],
  [15,7]
]
```

Difficulty:Medium  
Total Accepted:139.6K  
Total Submissions:376.5K  
Related Topics:Stack, Tree, BFS

### 解题思路
跟102题相比只要增加一个判断条件，满足条件就reverse即可。
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
    def zigzagLevelOrder(root: TreeNode): List[List[Int]] = {
        var res:List[List[Int]] = List()
        if(root==null) return res
        var que = new scala.collection.mutable.Queue[TreeNode]()
        que.enqueue(root)
        var count = 0
        while(!que.isEmpty){
            var len = que.size
            var r:List[Int] = List()
            for(i <- 0 until len){
                var temp = que.dequeue
                r = r :+ temp.value
                if(temp.left!=null) que.enqueue(temp.left)
                if(temp.right!=null) que.enqueue(temp.right)        
            }
            count += 1
            if(count%2==0){
                r= r.reverse
            }
            res = res :+ r
        }
        res
    }
}
```