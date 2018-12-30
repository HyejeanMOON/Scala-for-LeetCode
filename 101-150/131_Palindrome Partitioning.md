Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

Example:
```
Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```
Difficulty:Medium  
Total Accepted:124.8K  
Total Submissions:343.1K
Related Topics:Backtracking

### 解题思路
需要好好记住中间回溯的部分。中间部分是char之间的组合问题。
#### Scala
```scala
object Solution {
    def partition(s: String): List[List[String]] = {
        if(s=="") return List()
        var res:List[List[String]] = List()
        var out = new scala.collection.mutable.Stack[String]()
        res = bt(s,0,out,res)
        res
    }
    def bt(s:String,start:Int,out:scala.collection.mutable.Stack[String],res:List[List[String]]):List[List[String]]={
        var tempout = out
        var tempres = res
        if(start==s.length){
            tempres = tempres :+ tempout.toList.reverse
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
            tempstart += 1
            tempend -= 1
        }
        true
    }
}
```