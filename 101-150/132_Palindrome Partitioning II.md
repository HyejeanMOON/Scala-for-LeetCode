Given a string s, partition s such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of s.

Example:
```
Input: "aab"
Output: 1
Explanation: The palindrome partitioning ["aa","b"] could be produced using 1 cut.
```

Difficulty:Hard  
Total Accepted:84K  
Total Submissions:333.5K  
Related Topics:Dynamic Programming

### 解题思路



---

TLE!
#### Scala
```scala
object Solution {
    def minCut(s: String): Int = {
        var out = new scala.collection.mutable.Stack[String]()
        var res = scala.Int.MaxValue
        res = bt(s,0,out,res)
        if(res==scala.Int.MaxValue) res=0
        res
    }
    def bt(s:String,start:Int,out:scala.collection.mutable.Stack[String],res:Int):Int={
        var tempout = out
        var tempres = res
        if(start==s.length){
            tempres = scala.math.min(res,tempout.toList.length-1)
            return tempres
        }
        for(i <- start until s.length){
            if(isPali(s,start,i)){
                tempout.push(s.substring(start,i+1))
                tempres = bt(s,i+1,tempout,tempres)
                tempout.pop
            }
        }
        tempres
    }
    def isPali(s:String,start:Int,end:Int):Boolean={
        var tempstart = start
        var tempend = end
        while(tempstart<tempend){
            if(s.charAt(tempstart)!=s.charAt(tempend)) return false
            tempstart+=1
            tempend-=1
        }
        true
    }
}
```