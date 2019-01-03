Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

Example 1:
```
Input: s = "egg", t = "add"
Output: true
```
Example 2:
```
Input: s = "foo", t = "bar"
Output: false
```
Example 3:
```
Input: s = "paper", t = "title"
Output: true
```
Note:  
You may assume both s and t have the same length.

Difficulty:Easy  
Total Accepted:139.2K  
Total Submissions:398.7K  
Related Topics:Hash Tables


### 解题思路
- 这道题如果用哈希表的话，需要相互check的情况，会变得超级复杂，如果用长度为256的数组的话，可以轻松实现两边是否是一一对应的关系。  
- 这道题让我们求同构字符串，就是说原字符串中的每个字符可由另外一个字符替代，可以被其本身替代，相同的字符一定要被同一个字符替代，且一个字符不能被多个字符替代，即不能出现一对多的映射。根据一对一映射的特点，我们需要用两个哈希表分别来记录原字符串和目标字符串中字符出现情况，由于ASCII码只有256个字符，所以我们可以用一个256大小的数组来代替哈希表，并初始化为0，我们遍历原字符串，分别从源字符串和目标字符串取出一个字符，然后分别在两个哈希表中查找其值，若不相等，则返回false，若相等，将其值更新为i + 1，因为默认的值是0，所以我们更新值为i + 1，这样当 i=0 时，则映射为1，如果不加1的话，那么就无法区分是否更新了。

#### Scala
```scala
object Solution {
    def isIsomorphic(s: String, t: String): Boolean = {
        var sr = new scala.collection.mutable.ArrayBuffer[Int]()
        var tr = new scala.collection.mutable.ArrayBuffer[Int]()
        for(i <- 0 until 256){
            sr = sr :+ 0
            tr = tr :+ 0
        }
        if(s.length!=t.length) return false
        var len = s.length
        for(i <- 0 until len){
            var ss = s.charAt(i)
            var tt = t.charAt(i)
            if(sr(ss.toInt) != tr(tt.toInt)) return false
            sr(ss.toInt) = i+1
            tr(tt.toInt) = i+1
        }
        true
    }
}
```