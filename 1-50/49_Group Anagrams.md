Given an array of strings, group anagrams together.

Example:
```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
Note:

All inputs will be in lowercase.
The order of your output does not matter.

Difficulty:Medium  
Total Accepted:202.3K  
Total Submissions:518.4K  
Related Topics:Hash Table, String

### 解题思路
该题需要用到哈希表，把已经拍过序的string作为key，把实际的string作为value。哈希表的组成结构是Map[String,List[String]]。
#### Scala
```scala
object Solution {
    def groupAnagrams(strs: Array[String]): List[List[String]] = {
        var res:List[List[String]] = List()
        var record:Map[String,List[String]] = Map()
        for(s <- strs){
            var ss = s.sorted
            var temp = record.getOrElse(ss,List())
            temp = temp :+ s
            record += (ss -> temp)
        }
        var keys = record.keySet
        for(key <- keys){
            var temp = record.getOrElse(key,List())
            res = res :+ temp
        }
        res
    }
}
```