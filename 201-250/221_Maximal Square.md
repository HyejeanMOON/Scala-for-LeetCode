Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

Example:
```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```

Difficulty:Medium   
Total Accepted:89.5K  
Total Submissions:293.2K  
Related Topics:Dynamic Programming

### 解题思路
我们还可以进一步的优化时间复杂度到O(n2)，做法是使用DP，简历一个二维dp数组，其中dp[i][j]表示到达(i, j)位置所能组成的最大正方形的边长。我们首先来考虑边界情况，也就是当i或j为0的情况，那么在首行或者首列中，必定有一个方向长度为1，那么就无法组成长度超过1的正方形，最多能组成长度为1的正方形，条件是当前位置为1。边界条件处理完了，再来看一般情况的递推公式怎么办，对于任意一点dp[i][j]，由于该点是正方形的右下角，所以该点的右边，下边，右下边都不用考虑，关心的就是左边，上边，和左上边。这三个位置的dp值suppose都应该算好的，还有就是要知道一点，只有当前(i, j)位置为1，dp[i][j]才有可能大于0，否则dp[i][j]一定为0。当(i, j)位置为1，此时要看dp[i-1][j-1], dp[i][j-1]，和dp[i-1][j]这三个位置，我们找其中最小的值，并加上1，就是dp[i][j]的当前值了，这个并不难想，毕竟不能有0存在，所以只能取交集，最后再用dp[i][j]的值来更新结果res的值即可。
#### Scala
```scala
object Solution {
    def maximalSquare(matrix: Array[Array[Char]]): Int = {
        if(matrix.isEmpty || matrix(0).isEmpty) return 0
        var res = 0
        var len1 = matrix.length
        var len2 = matrix(0).length
        var dp = Array.ofDim[Int](len1,len2)
        for(i <- 0 until len1){
            for(j <- 0 until len2){
                dp(i)(j)=0
            }
        }
        for(i <- 0 until len1){
            for(j <- 0 until len2){
                if(i==0||j==0){
                    dp(i)(j)= matrix(i)(j)-'0'
                }else if(matrix(i)(j)=='1'){
                    dp(i)(j) = scala.math.min(dp(i-1)(j-1),scala.math.min(dp(i-1)(j),dp(i)(j-1))) +1
                }
                res = scala.math.max(dp(i)(j),res)
            }
        }
        res*res
    }
}
```
### 解题思路
下面这种解法进一步的优化了空间复杂度，此时只需要用一个一维数组就可以解决，为了处理边界情况，padding了一位，所以dp的长度是m+1，然后还需要一个变量pre来记录上一个层的dp值，我们更新的顺序是行优先，就是先往下遍历，用一个临时变量t保存当前dp值，然后看如果当前位置为1，则更新dp[i]为dp[i], dp[i-1], 和pre三者之间的最小值，再加上1，来更新结果res，如果当前位置为0，则重置当前dp值为0，因为只有一维数组，每个位置会被重复使用。

#### scala
```scala
object Solution {
    def maximalSquare(matrix: Array[Array[Char]]): Int = {
        if(matrix.isEmpty || matrix(0).isEmpty) return 0
        var len1 = matrix.length
        var len2 = matrix(0).length
        var pre = 0
        var res = 0
        var dp = new scala.collection.mutable.ArrayBuffer[Int]()
        for(i <- 0 to len1){
            dp = dp :+ 0
        }
        for(j <- 0 until len2){
            for(i <- 1 to len1){
                var t = dp(i)
                if(matrix(i-1)(j)=='1'){
                    dp(i) = scala.math.min(dp(i),scala.math.min(dp(i-1),pre))+1
                    res = scala.math.max(res,dp(i))
                }else{
                    dp(i)=0
                }
                pre = t
            }
        }
        res*res
    }
}
```