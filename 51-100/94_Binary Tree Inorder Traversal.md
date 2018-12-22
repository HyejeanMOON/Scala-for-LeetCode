Given a binary tree, return the inorder traversal of its nodes' values.

Example:
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```
Follow up: Recursive solution is trivial, could you do it iteratively?

Difficulty:Medium  
Total Accepted:312.4K  
Total Submissions:608.3K  
Related Topics:Hash Table, Stack, Tree

### 解题思路 
二叉树的中序遍历顺序为左-根-右，可以有递归和非递归来解，其中非递归解法又分为两种，一种是使用栈来接，另一种不需要使用栈。我们先来看递归方法，十分直接，对左子结点调用递归函数，根节点访问值，右子节点再调用递归函数。
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
    def inorderTraversal(root: TreeNode): List[Int] = {
        var res:List[Int] = List()
        res = dfs(root,res)
        res
    }
    def dfs(root:TreeNode,r:List[Int]):List[Int]={
        if(root==null) return r
        var res = r
        if(root.left!=null) res = dfs(root.left,res)
        res=res:+root.value
        if(root.right!=null) res = dfs(root.right,res)
    }
}
```

```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        ArrayList<Integer> res = new ArrayList<Integer>();
        dfs(root,res);
        return res;
    }
    public void dfs(TreeNode root, ArrayList<Integer> r){
        if(root==null) return;
        if(root.left!=null) dfs(root.left, r);
        r.add(root.val);
        if(root.right!=null) dfs(root.right,r);
    }
}
```



---


