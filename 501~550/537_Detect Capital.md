
Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:

All letters in this word are capitals, like "USA".
- All letters in this word are not capitals, like "leetcode".
- Only the first letter in this word is capital if it has more than one letter, like "Google".
- Otherwise, we define that this word doesn't use capitals in a right way.  
Example 1:
```
Input: "USA"
Output: True
```
Example 2:
```
Input: "FlaG"
Output: False
```
Note: The input will be a non-empty word consisting of uppercase and lowercase latin letters.




### 解题思路
首先为字符串里有多少个大写计数。再根据计数的结果进行分类判断。
#### Scala
```
object Solution {
    def detectCapitalUse(word: String): Boolean = {
        var result = false
        var capitalCount = 0
        for(w <- word){
            if(w.isUpper){
                capitalCount += 1
            }
        }
        if(capitalCount == word.length){
            result = true
        }
        if(capitalCount == 1 && word.charAt(0).isUpper){
            result = true
        }
        if(capitalCount == 0){
            result = true
        }
        result
    }
}
```