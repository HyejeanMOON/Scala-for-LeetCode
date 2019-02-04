Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.

Example 1:
```
Input: [1,12,-5,-6,50,3], k = 4
Output: 12.75
Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75
```
Note:  
1 <= k <= n <= 30,000.
Elements of the given array will be in the range [-10,000, 10,000].

Difficulty:Easy  
Total Accepted:26.1K  
Total Submissions:69.6K  
Related Topics:Array


### 解题思路
遍历所有子数组，然后找出最大值。
#### Scala
```scala
object Solution {
    def findMaxAverage(nums: Array[Int], k: Int): Double = {
        if(nums.length==1) return nums(0)
        var res = scala.Int.MinValue
        for(i <- 0 until nums.length-k+1){
            var temp = 0
            for(j <- i until i+k){
                temp += nums(j)
            }
            res = scala.math.max(res,temp)
        }
        println(res)
        println(k)
        var result:Double = res.toDouble/k
        result
    }
}
```