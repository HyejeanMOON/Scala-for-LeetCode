Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note:   
A word is defined as a character sequence consists of non-space characters only.

Example:
```
Input: "Hello World"
Output: 5
```

### 解题思路
遍历每个字符，如果遇到空格，则记录最大值并晴空count。为了防止无空格的字符串，当count不等于零时，则把count当作最大值。
#### Scala
```
object Solution {
    def lengthOfLastWord(s: String): Int = {
        var temp = s.trim
        var leng = temp.length
        var result = 0
        var count = 0       
        for(i <- 0 until leng){
            if(temp.charAt(i).toString == " "){
                 if(count > result) result = count
                count = 0
            }else{
                count += 1
            }
        }
        if(count != 0) result = count
        result
    }
}
```