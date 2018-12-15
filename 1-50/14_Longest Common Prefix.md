Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:
```
Input: ["flower","flow","flight"]
Output: "fl"
```
Example 2:
```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```
Note:

All given inputs are in lowercase letters a-z.

Difficulty:Easy  
Total Accepted:268.6K  
Total Submissions:849.7K  
Related Topics:String

### 解题思路
#### Scala
```scala
object Solution {
    def longestCommonPrefix(strs: Array[String]): String = {
        if(strs.length==0) return ""
        else if(strs.length==1) return strs(0)
        var res = ""
        var len = scala.Int.MaxValue
        for(s <- strs){
            if(len>s.length) len=s.length
        }
        for(i <- 0 until len){
            var p = strs(0).charAt(i)
            for(j <- 1 until strs.length){
                var pp = strs(j).charAt(i)
                if(p.toString!=pp.toString) return res 
            }
            res = res + p
        }
        res
    }
}
```
