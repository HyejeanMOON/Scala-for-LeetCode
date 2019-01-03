Given an integer, write a function to determine if it is a power of two.

### 解题思路
该题的意思是，给定一个数判断是否是2的次方。该题中，负数应该是false。
#### Scala
```scala
object Solution {
    def isPowerOfTwo(n: Int): Boolean = {
        var res = true
        var temp = n
        if(n == 0) return false
        if(n == 1) return true
        if(temp < 0) return false
        while(temp > 1){
            if(temp % 2 != 0) return false
            temp /= 2
        }
        res
    }
}
```