Given a range [m, n] where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

Example 1:
```
Input: [5,7]
Output: 4
```
Example 2:
```
Input: [0,1]
Output: 0
```

Difficulty:Medium  
Total Accepted:66.3K  
Total Submissions:191.9K  
Related Topics:Bit Manipulation

### 解题思路
http://www.cnblogs.com/grandyang/p/4431646.html
#### Scala
```scala
object Solution {
    def rangeBitwiseAnd(m: Int, n: Int): Int = {
        var d = scala.Int.MaxValue
        while((m&d) != (n&d)){
            d = d << 1
        }
        m&d
    }
}
```