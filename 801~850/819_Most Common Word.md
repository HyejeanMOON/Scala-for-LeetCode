Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words.  It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

Words in the list of banned words are given in lowercase, and free of punctuation.  Words in the paragraph are not case sensitive.  The answer is in lowercase.

Example:
```
Input: 
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
Output: "ball"
Explanation: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
 ```

Note:

- 1 <= paragraph.length <= 1000.  
- 1 <= banned.length <= 100.  
- 1 <= banned[i].length <= 10.  
- The answer is unique, and written in lowercase (even if its occurrences in paragraph may have uppercase symbols, and even if it is a proper noun.)
- paragraph only consists of letters, spaces, or the punctuation symbols !?',;.  
- Different words in paragraph are always separated by a space.  
- There are no hyphens or hyphenated words.
- Words only consist of letters, never apostrophes or other punctuation symbols.  

Difficulty:Easy  
Total Accepted:14.8K  
Total Submissions:30.4K  
Related Topics:String

### 解题思路
用正则表达式把符号都换成空字符，然后利用空格进行split。最后用map记录找出出现最多的string即可。

#### Scala
```Scala
import scala.util.matching.Regex
object Solution {
    def mostCommonWord(paragraph: String, banned: Array[String]): String = {
        val rex = "[!?',.;]".r
        var str = rex.replaceAllIn(paragraph,"")
        //正则表达式
        str = str.toLowerCase
        var s = str.split(" ")
        var record:Map[String,Int] = Map()
        for(ss <- s){
            var temp = record.getOrElse(ss,0)
            temp+=1
            record+=(ss -> temp)
        }
        for(b <- banned){
            record+=(b -> 0)
        }
        var mx = 0
        var keys = record.keySet
        var res = ""
        for(key <- keys){
            var temp = record.getOrElse(key,0)
            println(key)
            println(temp)
            println
            if(mx<temp){
                mx = temp
                res = key
            }
        }
        res
    }
}
```