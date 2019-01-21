Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

Example:
```
nums = [1, 2, 3]
target = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 7.
```
Follow up:   
What if negative numbers are allowed in the given array?
How does it change the problem?
What limitation we need to add to the question to allow negative numbers?

Related Topics:Dynamic Programming

###  解题思路
这道题是组合之和系列的第四道，我开始想当然的一位还是用递归来解，结果写出来发现TLE了，的确OJ给了一个test case为[4,1,2] 32，这个结果是39882198，用递归需要好几秒的运算时间，实在是不高效，估计这也是为啥只让返回一个总和，而不是返回所有情况，不然机子就爆了。而这道题的真正解法应该是用DP来做，解题思想有点像之前爬梯子的那道题Climbing Stairs，我们需要一个一维数组dp，其中dp[i]表示目标数为i的解的个数，然后我们从1遍历到target，对于每一个数i，遍历nums数组，如果i>=x, dp[i] += dp[i - x]。这个也很好理解，比如说对于[1,2,3] 4，这个例子，当我们在计算dp[3]的时候，3可以拆分为1+x，而x即为dp[2]，3也可以拆分为2+x，此时x为dp[1]，3同样可以拆为3+x，此时x为dp[0]，我们把所有的情况加起来就是组成3的所有情况了。
#### Scala
```scala
object Solution {
    def combinationSum4(nums: Array[Int], target: Int): Int = {
        var dp = new scala.collection.mutable.ArrayBuffer[Int]()
        for(i <- 0 to target){
            dp = dp :+ 0
        }
        dp(0)=1
        for(i <- 0 to target){
            for(n <- nums){
                if(i>=n) dp(i)+=dp(i-n)
            }
        }
        return dp(target)
    }
}
```