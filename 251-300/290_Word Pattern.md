Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

Examples:
```
pattern = "abba", str = "dog cat cat dog" should return true.
pattern = "abba", str = "dog cat cat fish" should return false.
pattern = "aaaa", str = "dog cat cat dog" should return false.
pattern = "abba", str = "dog dog dog dog" should return false.
```
Notes:  
You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

Difficulty:Easy  
Total Accepted:100.4K  
Total Submissions:300.5  
Related Topics: Hash Table

### 解题思路
首先需要判断pattern和分割后的str的长度是否一样。如果map里没有pattern则先判断map里面是否当前的string，要是有就返回false，没有则加入到map中，如果有则进行判断。如果不一致则返回false。
#### Scala
```Scala
object Solution {
    def wordPattern(pattern: String, str: String): Boolean = {
        var record:Map[Char,String] = Map()
        var s = str.split(" ")
        if(pattern.length != s.length) return false
        for(i <- 0 until pattern.length){
            var value = record.getOrElse(pattern.charAt(i),"NONE")
            if(value != "NONE"){    
                if(value != s(i)) return false
            }else{
                var keys = record.keySet
                for(k <- keys){
                    var t = record.getOrElse(k,"NONE")
                    if(t == s(i)) return false
                }
                record += (pattern.charAt(i) -> s(i))
            }
        }
        true
    }
}
```