Given a collection of distinct integers, return all possible permutations.

Example:
```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

Difficulty:Medium  
Total Accepted:242.7K  
Total Submissions:505.5K  
Related Topics:Array, Backtracking

### 解题思路
这道题跟39题和40题很相似，也是需要用到回溯。但是这道题需要回答全排的问题。这里的回溯循环是需要从零开始遍历，而且需要有个ArrayBuffer来记录该元素是否已经访问过。
#### Scala
```scala
object Solution {
    def permute(nums: Array[Int]): List[List[Int]] = {
        var res:List[List[Int]] = List()
        var out = new scala.collection.mutable.Stack[Int]()
        var visited = new scala.collection.mutable.ArrayBuffer[Int]()
        for(i <- 0 until nums.length){
            visited = visited :+ 0
        }
        res = find(nums,0,visited,out,res)
        res
    }
    def find(nums:Array[Int],level:Int,visited:scala.collection.mutable.ArrayBuffer[Int],out:scala.collection.mutable.Stack[Int],res:List[List[Int]]):List[List[Int]]={
        var tempres = res
        var tempout = out
        var tempv = visited
        if(level==nums.length){
            tempres = tempres :+ tempout.toList
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
