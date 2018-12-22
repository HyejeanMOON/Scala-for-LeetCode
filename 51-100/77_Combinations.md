Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

Example:
```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

Difficulty:Medium  
Total Accepted:147.2K  
Total Submissions:351.8K  
Related Topics:Backtracking

### 解题思路
这道题需要用回溯。跟其他的combinations题一样。  
这里需要注意的几点是：  
start要从1开始，因为题里的要求是不包含0。  
还有要设置一个num，用来终止递归以及正好获取两个数值。
#### Scala
```scala
object Solution {
    def combine(n: Int, k: Int): List[List[Int]] = {
        var res:List[List[Int]]=List()
        var out = new scala.collection.mutable.Stack[Int]()
        res = bt(n,k,1,0,out,res)
        res
    }
    def bt(n:Int,k:Int,start:Int,num:Int,out:scala.collection.mutable.Stack[Int],res:List[List[Int]]):List[List[Int]]={
        var tempres = res
        var tempout = out
        var tempnum = num
        if(num==k){           
            tempres=tempres:+tempout.toList
            return tempres
        }else{
            for(i <- start to n){
                tempout.push(i)
                tempres=bt(n,k,i+1,tempnum+1,tempout,tempres)
                tempout.pop
            }
        }
        tempres
    }
}
```