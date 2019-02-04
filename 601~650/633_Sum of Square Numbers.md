Given a non-negative integer c, your task is to decide whether there're two integers a and b such that a2 + b2 = c.

Example 1:
```
Input: 5
Output: True
Explanation: 1 * 1 + 2 * 2 = 5
```
Example 2:
```
Input: 3
Output: False
```

Difficulty:Easy  
Total Accepted:21.4K   
Total Submissions:66.3K  
Related Topics：Math

### 解题思路
因为这道题复杂度不会太高，所以就用了暴力搜索。首先求c的根。然后以0到根为范围，进行双指针搜索。其中加入判断，2倍left平方和2陪的right平方是否等于c。
#### Scala
```scala
object Solution {
    def judgeSquareSum(c: Int): Boolean = {
        if(c == 0) return true
        var sqr = (scala.math.sqrt(c)).toInt
        var left = 0
        var right = sqr
        while(left<right){
            var sum = left*left + right*right
            if(left*left*2 == c) return true
            else if(right*right*2 == c) return true 
            if(sum == c) return true
            else if(sum > c) right -= 1
            else if(sum < c) left += 1
        }
        false
    }
}
```
另一种方法： scala

```scala
object Solution {
    def judgeSquareSum(c: Int): Boolean = {
        var sqr = (scala.math.sqrt(c)).toInt
        for(i <- 0 to sqr){
            if(i*i == c) return true
            var t = c - i * i
            var tsqr = (scala.math.sqrt(t)).toInt
            if(tsqr*tsqr == t) return true
        }
        false
    }
}
```