Given a positive integer, check whether it has alternating bits: namely, if two adjacent bits will always have different values.

Example 1:
```
Input: 5
Output: True
Explanation:
The binary representation of 5 is: 101
```
Example 2:
```
Input: 7
Output: False
Explanation:
The binary representation of 7 is: 111.
```
Example 3:
```
Input: 11
Output: False
Explanation:
The binary representation of 11 is: 1011.
```
Example 4:
```
Input: 10
Output: True
Explanation:
The binary representation of 10 is: 1010.
```

Difficulty:Easy  
Total Accepted:21.3K  
Total Submissions:38.4K  
Related Topics:Bit Manipulation

### 解题思路
先把一个数转换成二进制，然后判断第i个和第i+1个是否一致。
#### Scala
```scala
object Solution {
    def hasAlternatingBits(n: Int): Boolean = {
        var temp = n
        var b = ""
        while(temp>0){
            var tt = temp%2
            b = tt.toString + b
            temp/=2
        }
        for(i <- 0 until b.length-1){
            if(b.charAt(i).toString==b.charAt(i+1).toString) return false
        }
        true
    }
}
```