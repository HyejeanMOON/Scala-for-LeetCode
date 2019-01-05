
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

Follow up:   
Could you do it without any loop/recursion in O(1) runtime?



### 解题思路
#### Scala
```scala
object Solution {
    def addDigits(num: Int): Int = {
        var res = 10
        var sum = num
        var flag = true
        if(num < 10) return num
        while(res >= 10){
            res = 0
            while(sum != 0){
                res += sum % 10
                sum /= 10
                //println(res)
            }
            sum = res
        }
        res
    }
}
```
#### Java
```java
class Solution {
    public int addDigits(int num) {
        int res = num;
        if(num < 10){
            return num;
        }
        while(res > 9){
            int r = res;
            res = 0;
            while(r>0){
                res = res + r%10;
                r = r/10;
            }
            //System.out.println(res);
        }
        return res;
    }
}
```


#### Scala
每九个一个循环。
```scala
object Solution {
    def addDigits(num: Int): Int = {
        return (num-1) % 9+1
    }
}
```