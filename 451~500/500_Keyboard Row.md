Given a List of words, return the words that can be typed using letters of alphabet on only one row's of American keyboard like the image below.

Example 1:
```
Input: ["Hello", "Alaska", "Dad", "Peace"]
Output: ["Alaska", "Dad"]
```
Note:  
You may use one character in the keyboard more than once.
You may assume the input string will only contain letters of alphabet.

Difficulty:Easy  
Total Accepted:58.6K  
Total Submissions:98K  
Related Topics： Hash Table

### 解题思路
用hash table解决该问题。同一行的字母设置成统一的value。然后对words进行遍历。如果该word的value都一致则记录。然后返回结果。
#### Scala
```scala
object Solution {
    def findWords(words: Array[String]): Array[String] = {
        var res:Array[String] = Array()
        var record:Map[String,Int] = Map()
        record += ("q" -> 1,"w" -> 1,"e" -> 1, "r" -> 1, "t" -> 1, "y" -> 1, "u" -> 1, "i" -> 1, "o" -> 1, "p" ->1)
        record += ("a" -> 2, "s" -> 2, "d" -> 2, "f" -> 2, "g" -> 2, "h" -> 2, "j" -> 2, "k" -> 2, "l" -> 2)
        record += ("z" -> 3, "x" -> 3, "c" -> 3, "v" -> 3, "b" -> 3, "n" -> 3, "m" -> 3)
        for(w <- words){
            var tempArray:Array[Int] = Array()
            for(ww <- w){
                var temp = ww.toLower.toString
                tempArray = tempArray :+ record.getOrElse(temp,0)
            }
            var flag = true
            for(i <- 1 until tempArray.length if flag){
                if(tempArray(i-1) != tempArray(i)){
                    flag = false
                }
            }
            if(flag){
                res = res :+ w
            }
        }
        res   
    }
}
```