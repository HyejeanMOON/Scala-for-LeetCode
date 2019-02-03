Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

Example 1:
```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```
Example 2:
```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

### 解题思路





---

TLE!
#### Scala
```
object Solution {
    def findAnagrams(s: String, p: String): List[Int] = {
        var slen = s.length
        var plen = p.length
        if(plen>slen) return List()
        var res:List[Int] = List()
        var pm:Map[Char,Int] = Map()
        for(pp <- p){
            var t = pm.getOrElse(pp,0)
            t+=1
            pm += (pp -> t)
        }
        for(i <- 0 to slen-plen){
            var m = pm
            for(j <- i until i+plen){
                var ss = s.charAt(j)
                var t = m.getOrElse(ss,0)
                t-=1
                m +=(ss -> t)
            }
            var sum = 0
            var flag = true
            for(v <- m.values) {
                if(v!=0) flag = false
            }
            if(flag) res= res:+i
        }
        res
    }
}
```