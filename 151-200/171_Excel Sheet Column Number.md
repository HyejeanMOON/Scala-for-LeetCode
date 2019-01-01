Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:
```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
```    
Example 1:
```
Input: "A"
Output: 1
```
Example 2:
```
Input: "AB"
Output: 28
```
Example 3:
```
Input: "ZY"
Output: 701
```

Difficulty:Easy  
Total Accepted:168K  
Total Submissions:345K  
Related Topics:Math

### 解题思路
一定要记住，用pow的时候要用toInt。因为pow的结果是Double。
#### Scala
```scala
object Solution {
    def titleToNumber(s: String): Int = {
        var res = 0
        var len = s.length
        var count = 1
        for(ss <- s){
            var l = ss - 'A' + 1
            var temp = (scala.math.pow(26,(len-count))*l.toInt).toInt
            count += 1
            res += temp
        }
        res
    }
}
```