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
该题的题目是要求计算可构建最长的回文，但从另一方面考虑的话，该题目实际是要求计算一个出现偶数次的个数。如果个数小于length，则加一。因为中间还可以加一个字母组成回文。
#### Scala
```scala
object Solution {
    def longestPalindrome(s: String): Int = {
        var record:Map[Char,Int] = Map()
        var leng = s.length
        var res = 0
        if(leng==1) return 1
        for(ss <- s){
            var temp = record.getOrElse(ss,0)
            temp += 1
            record += (ss -> temp)
        }
        var keys = record.keySet
        for(ks <- keys){
            res += record.getOrElse(ks,0) / 2
        }
        res = res * 2
        if(res < leng){
            res += 1
        }
        res
    }
}
```