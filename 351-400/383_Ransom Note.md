Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

Note:  
You may assume that both strings contain only lowercase letters.
```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

Difficulty:Easy  
Total Accepted:77.2K  
Total Submissions:161.6K  
Related Topics:String

### 解题思路
用map记录char的字数。
#### Scala
```scala
object Solution {
    def canConstruct(ransomNote: String, magazine: String): Boolean = {
        var record:Map[Char,Int] = Map()
        for(m <- magazine){
            var t = record.getOrElse(m,0)
            if(t==0) record += (m -> 1)
            else{
                t += 1
                record += (m -> t)
            }
        }
        for(r <- ransomNote){
            var t = record.getOrElse(r,0)
            if(t==0) return false
            else{
                t -= 1
                record += (r -> t)
            }
        }
        true
    }
}
```
