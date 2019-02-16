International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows: "a" maps to ".-", "b" maps to "-...", "c" maps to "-.-.", and so on.

For convenience, the full table for the 26 letters of the English alphabet is given below:
```
[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
```
Now, given a list of words, each word can be written as a concatenation of the Morse code of each letter. For example, "cab" can be written as "-.-.-....-", (which is the concatenation "-.-." + "-..." + ".-"). We'll call such a concatenation, the transformation of a word.

Return the number of different transformations among all words we have.

Example:
```
Input: words = ["gin", "zen", "gig", "msg"]
Output: 2
Explanation: 
The transformation of each word is:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."

There are 2 different transformations, "--...-." and "--...--.".

```
 

Note:

The length of words will be at most 100.
Each words[i] will have length in range [1, 12].
words[i] will only consist of lowercase letters.


Difficulty:Easy  
Total Accepted:15.6K  
Total Submissions:21.1K  

### 解题思路
#### Scala
```scala
object Solution {
    def uniqueMorseRepresentations(words: Array[String]): Int = {
        var res:List[String] = List()
        var mos:List[String]=List(".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--..")
        for(word <- words){
            var out = ""
            for(ww <- word){
                var temp = ww-'a'
                var t = mos(temp)
                out = out + t
            }
            res = res :+ out
        }
        var record:Map[String,Int] = Map()
        for(i <- 0 until res.length){
            var temp= record.getOrElse(res(i),0)
            temp += 1
            record += (res(i) -> temp)
        }
        var keys = record.keySet
        keys.size
    }
}
```