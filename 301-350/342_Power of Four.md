Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

Example:
Given num = 16, return true. Given num = 5, return false.

Follow up: Could you solve it without loops/recursion?

Difficulty:Easy  
Total Accepted:82.3K  
Total Submissions:210.6K  
Related Topics : Bit Manipulation
### 解题思路
#### Scala
```
object Solution {
    def isPowerOfFour(num: Int): Boolean = {
        var temp = num
        if(num <=0) return false
        while(temp>1){
            var t = temp % 4
            if(t!=0) return false
            temp /= 4
        }
        true
    }
}
```