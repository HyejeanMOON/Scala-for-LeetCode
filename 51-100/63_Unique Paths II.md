A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

Note: m and n will be at most 100.

Example 1:
```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```
Output: 2
```
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

Difficulty:Medium  
Total Accepted:135.2K  
Total Submissions:419.7K  
Related Topics:Array, Dynamic Programming

### 解题思路
这道题是之前那道 Unique Paths 不同的路径 的延伸，在路径中加了一些障碍物，还是用动态规划Dynamic Programming来解，不同的是当遇到为1的点，将该位置的dp数组中的值清零，其余和之前那道题并没有什么区别。
#### Scala
```scala
object Solution {
    def uniquePathsWithObstacles(obstacleGrid: Array[Array[Int]]): Int = {
        if(obstacleGrid.isEmpty || obstacleGrid(0).isEmpty) return 0
        var m = obstacleGrid.length
        var n = obstacleGrid(0).length
        if(obstacleGrid(0)(0)==1) return 0
        var dp = new scala.collection.mutable.ArrayBuffer[Int]()
        for(i <- 0 until n){
            dp = dp :+ 0
        }
        dp(0)=1
        for(i <- 0 until m){
            for(j <- 0 until n){
                if(obstacleGrid(i)(j)==1){
                    dp(j) = 0
                }else if(j>0){
                    dp(j) += dp(j-1)
                }
            }
        }
        dp(n-1)
    }
}
```