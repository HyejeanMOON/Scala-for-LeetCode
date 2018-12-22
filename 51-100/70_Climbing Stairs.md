You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.


Example 1:
```
Input: 2
Output:  2
Explanation:  There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps
```
Example 2:
```
Input: 3
Output:  3
Explanation:  There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

### 解题思路
用动态规划，dp[n] = dp[n-1] + dp[n-2]。因为每次只能爬1或2步，那么爬到第n层的方法要么是从第n-1层一步上来的，要不就是从n-2层2步上来的。
#### Scala
```scala
object Solution {
    def climbStairs(n: Int): Int = {
        if(n==0) return 0
        if(n==1) return 1
        if(n==2) return 2
        var dp = scala.collection.mutable.ArrayBuffer[Int](n+1)
        for(i <- 0 until n){
            dp = dp :+ 0
        }
        dp(0) = 0
        dp(1) = 1
        dp(2) = 2
        for(i <- 3 until n+1){
            dp(i) = dp(i-1) + dp(i-2)
        }
        var res = dp(n)
        res
    }
}
```