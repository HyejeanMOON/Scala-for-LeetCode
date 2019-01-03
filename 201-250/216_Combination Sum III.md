Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

Note:

All numbers will be positive integers.
The solution set must not contain duplicate combinations.  

Example 1:
```
Input: k = 3, n = 7
Output: [[1,2,4]]
```
Example 2:
```
Input: k = 3, n = 9
Output: [[1,2,6], [1,3,5], [2,3,4]]
```

Difficulty:Medium  
Total Accepted:91K  
Total Submissions:191.2K  
Related Topics:Array, Backtracking

### 解题思路
这道题也需要用回溯法。  
需要注意的地方是return的地方。如果一共遍历了三个数的话，进行判断是否等于n，如果等于加入到结果中，不是则直接返回。
#### Scala
```scala
object Solution {
    def combinationSum3(k: Int, n: Int): List[List[Int]] = {
        var res:List[List[Int]] = List()
        var out = new scala.collection.mutable.Stack[Int]()
        res = bt(k,n,1,0,out,res)
        res
    }
    def bt(k:Int,n:Int,start:Int,num:Int,out:scala.collection.mutable.Stack[Int],res:List[List[Int]]):List[List[Int]]={
        var tempout = out
        var tempres = res
        if(num==k){
            if(tempout.toArray.sum==n){
                tempres = tempres:+tempout.toList
                return tempres
            }
            return tempres
        }else{
            for(i <- start to 9){
                tempout.push(i)
                tempres=bt(k,n,i+1,num+1,tempout,tempres)
                tempout.pop
            }
        }
        tempres
    }
}
```