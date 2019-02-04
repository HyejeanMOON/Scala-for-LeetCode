Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of new tree.

Example 1:
```
Input: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
Output: 
Merged tree:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
```	 
Note:  
The merging process must start from the root nodes of both trees.



### 解题思路
用递归的方式，挨个搜索树。
#### Scala
```
/**
 * Definition for a binary tree node.
 * class TreeNode(var _value: Int) {
 *   var value: Int = _value
 *   var left: TreeNode = null
 *   var right: TreeNode = null
 * }
 */

object Solution {
  def mergeTrees(t1: TreeNode, t2: TreeNode): TreeNode = {
    if (t1 == null) {
      if (t2 == null) null
      else t2
    } else {
      if (t2 == null) t1
      else {
        val mt = new TreeNode(t1._value + t2._value)
        mt.left = mergeTrees(t1.left, t2.left)
        mt.right = mergeTrees(t1.right, t2.right)
        mt
      }
    }
  }
}
```
#### Java
```java
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
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if(t1 == null){
            if(t2 == null) return null;
            else return t2;
        }else{
            if(t2 == null) return t1;
            else{
                TreeNode mer = new TreeNode(t1.val + t2.val);
                mer.left = mergeTrees(t1.left,t2.left);
                mer.right = mergeTrees(t1.right,t2.right);
                return mer;
            }
        }
    }
}
```