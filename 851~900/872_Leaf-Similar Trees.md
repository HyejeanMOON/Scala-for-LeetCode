Consider all the leaves of a binary tree.  From left to right order, the values of those leaves form a leaf value sequence.



For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).

Two binary trees are considered leaf-similar if their leaf value sequence is the same.

Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.

 

Note:

Both of the given trees will have between 1 and 100 nodes.


Difficulty:Easy  
Total Accepted:6.8K  
Total Submissions:10.6K  
Related Topics:Tree, DFS

### 解题思路
用dfs记录，然后挨个比较。
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
    def leafSimilar(root1: TreeNode, root2: TreeNode): Boolean = {
        if(root1==null && root2==null) return true
        else if(root1==null && root2!=null) return false
        else if(root1!=null && root2==null) return true
        var res1:Array[Int] = Array()
        var res2:Array[Int] = Array()
        res1 = dfs(root1,res1)
        res2 = dfs(root2,res2)
        if(res1.length!=res2.length) return false
        for(i <- 0 until res1.length){
            if(res1(i)!=res2(i)) return false
        }
        true
    }
    def dfs(root:TreeNode,r:Array[Int]):Array[Int]={
        if(root==null) return r
        var res = r
        if(root.left==null && root.right==null) res=res:+root.value
        if(root.left!=null) res=dfs(root.left,res)
        if(root.right!=null) res=dfs(root.right,res)
        res
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
    public boolean leafSimilar(TreeNode root1, TreeNode root2) {
        if(root1==null && root2==null) return true;
        else if(root1==null && root2!=null) return false;
        else if(root1!=null && root2==null) return false;
        ArrayList<Integer> res1 = new ArrayList<Integer>();
        ArrayList<Integer> res2 = new ArrayList<Integer>();
        res1 = dfs(root1,res1);
        res2 = dfs(root2,res2);
        if(res1.toArray().length!=res2.toArray().length) return false;
        for(int i=0; i<res1.toArray().length; i++){
            if(res1.toArray()[i]!=res2.toArray()[i]) return false;
        }
        return true;
        
    }
    public ArrayList<Integer> dfs(TreeNode root, ArrayList<Integer> res) {
        if(root==null) return res;
        if(root.left==null && root.right==null) res.add(root.val);
        if(root.left!=null) res = dfs(root.left,res);
        if(root.right!=null) res = dfs(root.right,res);
        return res;
    }
}
```