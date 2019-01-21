Given a positive integer num, write a function which returns True if num is a perfect square else False.

Note:  
Do not use any built-in library function such as sqrt.

Example 1:
```
Input: 16
Returns: True
```
Example 2:
```
Input: 14
Returns: False
```

### 解题思路
很简单的数学题。就是判断开方以后的double值和int值是不是一样。
#### Scala
```scala
object Solution {
    def isPerfectSquare(num: Int): Boolean = {
        var temp:Double = scala.math.sqrt(num)
        var tempInt:Int = temp.toInt
        var res = false
        if(temp == tempInt) res = true
        else res = false
        res
    }
}
```

#### Java
```java
class Solution {
    public boolean isPerfectSquare(int num) {
        double temp = Math.sqrt(num);
        int tempInt = (int)temp;
        int tempNum = tempInt*tempInt;
        if(tempNum == num) return true;
        else return false;
    }
}
```