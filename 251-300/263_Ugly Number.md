Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 6, 8 are ugly while 14 is not ugly since it includes another prime factor 7.

Note:

1 is typically treated as an ugly number.
Input is within the 32-bit signed integer range.

### 解题思路
这道题让我们检测一个数是否为丑陋数，所谓丑陋数就是其质数因子只能是2,3,5。那么最直接的办法就是不停的除以这些质数，如果剩余的数字是1的话就是丑陋数。
#### Scala
```scala
object Solution {
    def isUgly(num: Int): Boolean = {
        if(num <= 0) return false
        if(num==1) return true
        var temp = num
        while(temp != 1){
            if(temp%2 == 0) temp /= 2
            else if(temp%3 == 0) temp /=3
            else if(temp%5 == 0) temp /=5
            else return false
        }
        true
    }
}
```