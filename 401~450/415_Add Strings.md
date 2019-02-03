Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.

Note:

1. The length of both num1 and num2 is < 5100.
1. Both num1 and num2 contains only digits 0-9.
1. Both num1 and num2 does not contain any leading zero.
1. You must not use any built-in BigInteger library or convert the inputs to integer directly.

### 解题思路
该题目的要求是计算和，但是不能用直接toInt的方式。所以在这里要用到ascii码，利用这个让每个char显示出自己本身的数字。其他方面都是很普通的求和题。
#### Scala
```scala
object Solution {
    def addStrings(num1: String, num2: String): String = {
        var leng1 = num1.length
        var leng2 = num2.length
        var i = leng1 - 1
        var j = leng2 - 1
        var carry = 0
        var res = ""
        while(i >= 0 || j >= 0){
            var tempA = 0
            var tempB = 0
            if(i >=0){
                tempA = num1.charAt(i) - '0'
                i -= 1            
            }
            if(j >= 0){
                tempB = num2.charAt(j) -'0'
                j -= 1
            }
            var sum = tempA + tempB + carry          
            res = (sum%10).toString + res
            carry = sum / 10
        }
       if(carry == 1){
           res = "1" + res
       }
        res
    }
}
```