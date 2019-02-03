Given a string and an integer k, you need to reverse the first k characters for every 2k characters counting from the start of the string. If there are less than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and left the other as original.  

Example:
```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```
Restrictions:  
The string consists of lower English letters only.
Length of the given string and k will in the range [1, 10000]

###  解题思路
如果单纯的遍历每个字符的话会LTE，所以要用substring的方式。该题中，偶数的时候反转，奇数时正常。然后最后把余数部分处理好就可以了。
#### Scala
```scala
object Solution {
    def reverseStr(s: String, k: Int): String = {
        var leng = s.length
        var res = ""
        var div = leng/k
        var t = leng%k
        for(i <- 0 until div){
            if(i%2 == 0){
                res = res + s.substring(k*i,k*(i+1)).reverse
            }else{
                res = res + s.substring(k*i,k*(i+1))
            }
        }
        if(div%2 == 0){
            res = res + s.substring(k*div,k*div+t).reverse
        }else{
            res = res + s.substring(k*div,k*div+t)
        }
        res
    }
}
```