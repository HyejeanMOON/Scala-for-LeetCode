Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

Example:  
Given a = 1 and b = 2, return 3.


### 解题思路
**  
简而言之就是用异或算不带进位的和，用与并左移1位来算进位，然后把两者加起来即可
#### Scala
```scala
object Solution {
    def getSum(a: Int, b: Int): Int = {
        if(a==0) return b
        if(b==0) return a
        var sum = a ^ b
        var carry = (a&b) << 1
        getSum(sum,carry)
    }
}
```