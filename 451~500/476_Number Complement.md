Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.

Note:  
The given integer is guaranteed to fit within the range of a 32-bit signed integer.
You could assume no leading zero bit in the integer’s binary representation.  
Example 1:  
```
Input: 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.
```
Example 2:
```
Input: 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.
```
### 解题思路
该题比较典型，简单。把num分解成2进制，没算一位就置反。也就是把1换成0，把0换成1。然后把2乘进去相加。
#### Scala
```scala
object Solution {
    def findComplement(num: Int): Int = {
        var res = 0
        var count = 0
        var tempNum = num
        while(tempNum > 0){
            var temp = tempNum%2
            if(temp==1) temp=0
            else temp=1
            res += temp*(scala.math.pow(2,count)).toInt
            count += 1
            tempNum /= 2
        }
        res
    }
}
```