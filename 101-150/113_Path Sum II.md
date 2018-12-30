
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

Note: A leaf is a node with no children.

Example:
```
Given the below binary tree and sum = 22,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
```
Return:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

Difficulty:Medium  
Total Accepted:166.2K  
Total Submissions:461.3K  
Related Topics: Tree, DFS

### 解题思路
特别经典的一道题，一定要记住。  
使用dfs，递归以及回溯法。  
但是基本思想都一样，还是需要用深度优先搜索DFS，只不过数据结构相对复杂一点，需要用到二维的vector，而且每当DFS搜索到新节点时，都要保存该节点。而且每当找出一条路径之后，都将这个保存为一维vector的路径保存到最终结果二位vector中。并且，每当DFS搜索到子节点，发现不是路径和时，返回上一个结点时，需要把该节点从一维vector中移除。
#### Scala
```scala
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
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if(root == null) return res;
        List<Integer> temp = new ArrayList<Integer>();
        dfs(root, res, temp, sum);
        return res;
    }
    private void dfs(TreeNode root, List<List<Integer>> res, List<Integer> temp, int sum) {
        temp.add(root.val);
        sum -= root.val;
        if(root.left == null && root.right == null)  //递归结束条件
            if(sum == 0) res.add(new ArrayList<>(temp));  //满足路径和等于 sum，添加到结果集中去
        if(root.left != null) dfs(root.left, res, temp, sum);
        if(root.right != null) dfs(root.right, res, temp, sum);
        temp.remove(temp.size()-1);  //回溯
    }
}

```

