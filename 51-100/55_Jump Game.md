Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.
```
For example:
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.
```

Difficulty:Medium  
Total Accepted:159.5K  
Total Submissions:540.1K  
Related Topics: Array, Greedy

### 解题思路
这道题说的是有一个非负整数的数组，每个数字表示在当前位置的基础上最多可以走的步数，求判断能不能到达最后一个位置，开始我以为是必须刚好到达最后一个位置，超过了不算，其实是理解题意有误，因为每个位置上的数字表示的是最多可以走的步数而不是像玩大富翁一样摇骰子摇出几一定要走几步。那么我们可以用动态规划Dynamic Programming来解，我们维护一个一位数组dp，其中dp[i]表示走道i位置时剩余的最大步数，那么递推公式为：dp[i] = max(dp[i - 1], A[i - 1]) - 1，如果当某一个时刻dp数组的值为负了，说明无法抵达当前位置，则直接返回false，最后我们判断dp数组最后一位是否为非负数即可知道是否能抵达该位置。
#### Scala
```scala
object Solution {
    def canJump(nums: Array[Int]): Boolean = {
        var dp = scala.collection.mutable.ArrayBuffer[Int]()
        var len = nums.length
        for(i <- 0 until len){
            dp = dp :+ 0
        }
        for(i <- 1 until len){
            dp(i) = scala.math.max(dp(i-1),nums(i-1)) -1
            if(dp(i)<0) return false
        }
        dp(len-1)>=0
    }
}
```