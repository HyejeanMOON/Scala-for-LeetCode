We define the Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself.

Now, given an integer n, write a function that returns true when it is a perfect number and false when it is not.
Example:
```
Input: 28
Output: True
Explanation: 28 = 1 + 2 + 4 + 7 + 14
```
Note:   
The input number n will not exceed 100,000,000. (1e8)

Difficulty:Easy  
Total Accepted:21.8K  
Total Submissions:66.9K  
Related Topics:Math

### 解题思路
简单的题，循环查找就好了。  
首先求它的根，然后把根以内的整数挨个查找一遍就可以了。还有算法中把res设为1的原因是任何一个数都有1，所以直接加进去，以后就不用再考虑它了。
#### Scala
```scala
object Solution {
    def checkPerfectNumber(num: Int): Boolean = {
        if(num<2) return false    
        var res = 1
        var sqr = (scala.math.sqrt(num)).toInt
        var n = 2
        while(n<=sqr){
            if(num%n==0){
                res += n
                if(n*n!=num){
                    res += num/n
                }
                //println(res)
            }
            n+=1
        }      
        if(res==num) return true
        false      
    }
}
```