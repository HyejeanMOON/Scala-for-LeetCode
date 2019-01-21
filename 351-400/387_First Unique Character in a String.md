Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

Note:  
Assume the length of given string will not exceed 1,010.

Example:
```
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

### 解题思路
首先遍历一次字符串来记录Char出现的次数。然后第二次遍历，如果value是1则返回它的position。
#### Scala
```scala
object Solution {
    def firstUniqChar(s: String): Int = {
        var record:Map[Char,Int] = Map()
        for(ss <- s){
            var temp = record.getOrElse(ss,0)
            temp += 1
            record += (ss -> temp)
        }
        var leng = s.length
        for(i <- 0 until leng){
            var tempChar = s.charAt(i)
            if(record.getOrElse(tempChar,0) == 1){
                return i
            }
        }
        -1
    }
}
```