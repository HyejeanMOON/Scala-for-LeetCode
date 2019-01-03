Given two strings s and t, write a function to determine if t is an anagram of s.

For example,

s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?

Difficulty:Easy  
Total Accepted:214.1K  
Total Submissions:449K  
Related Topics:Hash Table, Sort

### 解题思路
建立两个哈希表，然后进行对比。
#### Scala
```scala
object Solution {
    def isAnagram(s: String, t: String): Boolean = {
        var r1:Map[Char,Int] = Map()
        var r2:Map[Char,Int] = Map()
        for(ss <- s){
            var temp = r1.getOrElse(ss,0)
            temp += 1
            r1 += (ss -> temp)
        }
        for(tt <- t){
            var temp = r2.getOrElse(tt,0)
            temp += 1
            r2 += (tt -> temp)
        }
        var k1 = r1.keySet.toArray.sorted
        var k2 = r2.keySet.toArray.sorted
        if(k1.length!=k2.length) return false
        for(i <- 0 until k1.length){
            if(k1(i)!=k2(i)) return false
            else {
                var t1 = r1.getOrElse(k1(i),0)
                var t2 = r2.getOrElse(k2(i),0)
                if(t1!=t2) return false
            }
        }
        true
    }
}
```