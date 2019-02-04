Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

Example 1:
```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```
Note: In the string, each word is separated by single space and there will not be any extra space in the string.


### 解题思路
先把字符串依据“空格”进行分割，再把分割出来的每个字符串进行颠倒，然后最后进行拼接即可。

#### Scala
```
object Solution {
    def reverseWords(s: String): String = {
        var result:String = ""
        var sSplit = s.split(" ")
        for(i <- 0 until sSplit.length){
            var temp = sSplit(i).reverse
            result = result + " " + temp
        }
        result = result.trim
        result
    }
}
```