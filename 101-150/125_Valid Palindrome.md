Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

```
For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.
```

Note:  
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.


### 解题思路
先把字符串中非子母和数字的char给剔除掉，组成新的字符串。  
并对新的字符串前后进行对比。如果不一致，直接return false。  
整个遍历循环以后都相等，则返回true。
#### Scala
```scala
object Solution {
    def isPalindrome(s: String): Boolean = {
        var temp = ""
        for(ss <- s){
            if(ss.isLetterOrDigit){
                temp = temp + ss.toLower
            }
        }
        var leng = temp.length
        for(i <- 0 until leng/2){
            if(temp.charAt(i) != temp.charAt(leng-i-1) ){
                return false
            }
        }
        true
    }
}
```