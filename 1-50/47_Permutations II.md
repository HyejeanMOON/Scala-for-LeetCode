Given a collection of numbers that might contain duplicates, return all possible unique permutations.

Example:
```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

Difficulty:Medium  
Total Accepted:167.6K  
Total Submissions:471.8K  
Related Topics:Backtracking


### 解题思路
这道题跟46道题的区别是这道题有重复的元素。整体算法是跟上道题一样，只是把res的数据类型换成set，从而去除重复的值。
#### Scala
```scala
object Solution {
    def permuteUnique(nums: Array[Int]): List[List[Int]] = {
        var res:Set[List[Int]] = Set()
        var out = new scala.collection.mutable.Stack[Int]()
        var visited = new scala.collection.mutable.ArrayBuffer[Int]()
        for(i <- 0 until nums.length){
            visited = visited :+ 0
        }
        res = find(nums,0,visited,out,res)
        res.toList
    }
    def find(nums:Array[Int],level:Int,visited:scala.collection.mutable.ArrayBuffer[Int],out:scala.collection.mutable.Stack[Int],res:Set[List[Int]]):Set[List[Int]]={
        var tempres = res
        var tempout = out
        var tempv = visited
        if(level==nums.length){
            tempres = tempres + tempout.toList
            return tempres
        }
        else{
            for(i <- 0 until nums.length){
                if(tempv(i)==0){
                    tempv(i)=1
                    tempout.push(nums(i))
                    tempres = find(nums,level+1,tempv,tempout,tempres)
                    tempout.pop
                    tempv(i)=0
                }
            }
        }
        tempres
    }
}
```
