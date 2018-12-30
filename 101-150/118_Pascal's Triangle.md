Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.


In Pascal's triangle, each number is the sum of the two numbers directly above it.

Example:
```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

Difficulty:Easy  
Total Accepted:172.4K  
Total Submissions:427.2K  
Related Topics:Array

### 解题思路
这道题需要分情况考虑。首先是等于1的情况。然后是等于2的情况。最后是大于等于3的情况。
#### Scala
```scala
object Solution {
    def generate(numRows: Int): List[List[Int]] = {
        var res:List[List[Int]] = List()
        if(numRows==1) return List(List(1))
        if(numRows==2) return List(List(1),List(1,1))
        if(numRows>=3){
            res = res :+ List(1)
            res = res :+ List(1,1)
            for(i <- 2 until numRows){
                var temp:List[Int] = List()
                temp = temp :+ 1
                for(j <- 0 until res(i-1).length-1){
                    var t = res(i-1)(j) + res(i-1)(j+1)
                    temp = temp :+ t
                }
                temp = temp :+ 1
                res = res :+ temp
            }
        }
        res
    }
}
```