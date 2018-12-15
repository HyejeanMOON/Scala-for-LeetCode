Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

Each number in candidates may only be used once in the combination.

Note:

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.  

Example 1:
```
Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```
Example 2:  
```
Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]
```

Difficulty:Medium  
Total Accepted:155.4K  
Total Submissions:426.1K  
Related Topics:Array, Backtracking

### 解题思路
这道题需要用回溯。跟上道题39题相似。但是这道题的要求是数组中的元素只允许用一次。而且数组中还会有重复的数组出现。为了防止被重复记录，使用Set。还需要注意的是在回溯循环中的递归中的起点这道题是i+1，因为只允许使用一次。而上一道是i，因为可以重复使用。
#### Scala
```scala
object Solution {
    def combinationSum2(candidates: Array[Int], target: Int): List[List[Int]] = {
        var res:Set[List[Int]] = Set()
        var out = new scala.collection.mutable.Stack[Int]()
        res = find(candidates,target,0,out,res)
        res.toList
    }
    def find(can:Array[Int],target:Int,start:Int,out:scala.collection.mutable.Stack[Int],res:Set[List[Int]]):Set[List[Int]]={
        var tempres = res
        var tempout = out
        if(target<0) return tempres
        else if(target==0) tempres = tempres+tempout.toArray.sorted.toList
        else{
            for(i <- start until can.length){
                tempout.push(can(i))
                tempres = find(can,target-can(i),i+1,tempout,tempres)
                tempout.pop
            }
        }
        tempres
    }
}
```