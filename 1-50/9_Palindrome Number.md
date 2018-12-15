Determine whether an integer is a palindrome. Do this without extra space.

Difficulty:Easy  
Total Accepted:311.5K  
Total Submissions:872.1K  
Related Topics:Math

### 解题思路
 这道验证回文数字的题不能使用额外空间，意味着不能把整数变成字符，然后来验证回文字符串。而是直接对整数进行操作，我们可以利用取整和取余来获得我们想要的数字，比如 1221 这个数字，如果 计算 1221 / 1000， 则可得首位1， 如果 1221 % 10， 则可得到末尾1，进行比较，然后把中间的22取出继续比较。
#### Scala
```scala
object Solution {
    def isPalindrome(x: Int): Boolean = {
        if(x<0) return false
        var temp = x
        var div = 1
        while(temp/div >= 10) div = div*10
        while(temp>0){
            var left = temp /div
            var right = temp % 10
            if(left!=right) return false
            temp = (temp%div)/10
            div /= 100
        }
        true
    }
}
```


#### python
```python
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x<0:
            return False
        leng = len(str(x))
        s=str(x)
        if leng==1 :
            return True
        for i in range(0,leng//2):
            index=leng-1-i
            if s[i]!=s[index] :
                return False
        return True
```