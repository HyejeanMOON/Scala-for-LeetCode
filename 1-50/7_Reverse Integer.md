Given a 32-bit signed integer, reverse digits of an integer.

Example 1:
```
Input: 123
Output:  321
```
Example 2:
```
Input: -123
Output: -321
```
Example 3:
```
Input: 120
Output: 21
```
Note:  
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.


### 解题思路
该题很典型。余数相乘相加来解决。但是题中有一个要求就是，如果超过int的MaxValue的话要求返回0。所以把返回值暂时设置成Long。如果判断res超过int的MaxValue则返回0。
#### Scala
```scala
object Solution {
    def reverse(x: Int): Int = {
        if(x>scala.Int.MaxValue) return 0
        var res:Long = 0
        var temp = x
        var isMinus = false
        if(temp<0){
            isMinus = true
            temp = 0 -temp
        }
        while(temp>0){
            var t = temp%10
            res = res*10 + t
            temp /= 10
        }
        if(res > scala.Int.MaxValue) return 0
        if(isMinus){
            res = 0 - res
        }
        res.toInt   
    }
}
```


#### python
```python
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        res=0L
        if x > 0:
            while x > 0:
                tmp=x%10
                res=res*10+tmp
                x=x//10
        else:
            x=0-x
            while x > 0:
                tmp=x%10
                res=res*10+tmp
                x=x//10
            res=0-res
        if res < 2147483648 and res > -2147483648 :
            return res
        else:
            return 0
        
```
#### python
利用的是字符串反转。

```python
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        x = int(str(x)[::-1]) if x >= 0 else - int(str(-x)[::-1])
        return x if x < 2147483648 and x >= -2147483648 else 0
        
```
