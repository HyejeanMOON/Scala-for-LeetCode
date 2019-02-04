You are given a string representing an attendance record for a student. The record only contains the following three characters:
1. 'A' : Absent.
1. 'L' : Late.
1. 'P' : Present.
A student could be rewarded if his attendance record doesn't contain more than one 'A' (absent) or more than two continuous 'L' (late).

You need to return whether the student could be rewarded according to his attendance record.

Example 1:
```
Input: "PPALLP"
Output: True
```
Example 2:
```
Input: "PPALLL"
Output: False
```

### 解题思路
题目要求是学生不能有一次以上的缺席和连续两次以上的迟到。缺席只要计数就可以了。关于迟到是先计数如果中间有出席和缺席就把关于迟到的计数清零。如果达到连续三次就输出false。

#### Scala
```
object Solution {
    def checkRecord(s: String): Boolean = {
        var result = true
        var p = 0
        var a = 0
        var l = 0
        for(ss <- s){
            var temp = ss.toString
            if(temp == "A") {
                a += 1
                l = 0
            }
            if(temp == "P"){
                l = 0
            }
            if(temp == "L"){
                l += 1
                if(l > 2){
                    result = false
                }
            }
        }
        if(a > 1){
            result = false
        }
        result
    }
}
```