Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example 1:
```
[[1,3,1],
 [1,5,1],
 [4,2,1]]
 ```
Given the above grid map, return 7. Because the path 1→3→1→1→1 minimizes the sum.

Difficulty:Medium  
Total Accepted:144.6K  
Total Submissions:355.9K  
Related Topics:Array, Dynamic Programming

### 解题思路
这道题跟之前那道 Dungeon Game 地牢游戏 没有什么太大的区别，都需要用动态规划Dynamic Programming来做，这应该算是DP问题中比较简单的一类，我们维护一个二维的dp数组，其中dp[i][j]表示当前位置的最小路径和，递推式也容易写出来 dp[i][j] = grid[i][j] + min(dp[i - 1][j]。
#### Java
```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m][n];
        dp[0][0] = grid[0][0];
        for(int i=1; i<m; i++) dp[i][0] = dp[i-1][0]+grid[i][0];
        for(int j=1; j<n; j++) dp[0][j] = dp[0][j-1] + grid[0][j];
        for(int i=1; i<m; i++){
            for(int j=1; j<n; j++){
                dp[i][j] = grid[i][j] + Math.min(dp[i-1][j],dp[i][j-1]);
            }
        }
        return dp[m-1][n-1];
    }
}
```