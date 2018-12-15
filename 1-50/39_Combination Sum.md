
Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

Note:

All numbers (including target) will be positive integers.  
The solution set must not contain duplicate combinations.
Example 1:
```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```
Example 2:
```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

Difficulty:Medium  
Total Accepted:224.6K  
Total Submissions:534.4K  
Related Topics:Array, Backtracking

### 解题思路
这道题需要用回溯。用回溯的方式挨个去查找数组中是否有满足要求的。这道题需要注意的是可以有重复的使用。下一道题中要求是不能重复使用。总体的思路是一样的。
#### Scala
```scala
object Solution {
    def combinationSum(candidates: Array[Int], target: Int): List[List[Int]] = {
        var res:List[List[Int]] = List()    
        var out = new scala.collection.mutable.Stack[Int]()
        res=dfs(candidates,target,0,out,res)
        res
    }
    def dfs(num:Array[Int],target:Int,start:Int,out:scala.collection.mutable.Stack[Int],res:List[List[Int]]):List[List[Int]]={
        var tempres = res
        var tempout = out
        if(target<0) return tempres
        else if(target==0) tempres = tempres :+ tempout.toList
        else{
            for(i <- start until num.length){
                tempout.push(num(i))
                tempres=dfs(num,target-num(i),i,tempout,tempres)
                tempout.pop
            }
        }
        tempres
    }
}
```