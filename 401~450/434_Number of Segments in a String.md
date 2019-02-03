Count the number of segments in a string, where a segment is defined to be a contiguous sequence of non-space characters.

Please note that the string does not contain any non-printable characters.

Example:
```
Input: "Hello, my name is John"
Output: 5
```

Difficulty:Easy  
Total Accepted:37.9K  
Total Submissions:103.7K  
Related Topics:String

### 解题思路
该题用String的split就可以。这里有一个注意的地方是，如果有多个空格，算一个。所以需要用到trim把多余的空格给去除掉。
#### Scala
```scala
object Solution {
    def countSegments(s: String): Int = {
        if(s.trim == "") return 0
        var sp = s.split(" ")
        var count = 0
        for(ss <- sp){
            if(ss.trim!="") count+=1
        }
        count
    }
}
```