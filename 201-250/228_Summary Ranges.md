Given a sorted integer array without duplicates, return the summary of its ranges.

Example 1:
```
Input:  [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
Explanation: 0,1,2 form a continuous range; 4,5 form a continuous range.
```
Example 2:
```
Input:  [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
Explanation: 2,3,4 form a continuous range; 8,9 form a continuous range.
```

Difficulty:Medium  
Total Accepted:103.7K  
Total Submissions:315.8K  
Related Topics:Array

### 解题思路
相当普通的一道题。
#### Scala
```scala
object Solution {
    def summaryRanges(nums: Array[Int]): List[String] = {
        if(nums.length==0) return List()
        var res:List[String] = List()
        var record:List[List[Int]] = List()
        var len = nums.length
        var out:List[Int] = List()
        out = out:+nums(0)
        for(i <- 1 until len){
            if(nums(i)-nums(i-1)==1) out=out:+nums(i)
            else{
                record=record:+out
                out=List()
                out=out:+nums(i)
            }
        }
        record=record:+out
        println(record.length)
        for(r <- record){
            var l = r.length
            if(l==1) res=res:+r(0).toString
            else {
                var temp = r(0).toString + "->" + r(l-1).toString
                res=res:+temp
            }
        }
        res
    }
}
```