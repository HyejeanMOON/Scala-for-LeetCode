Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle
```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).
```
Note:

Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

Difficulty:Medium  
Total Accepted:134.4K    
Total Submissions:381.6K  
Related Topics: Array, Dynamic Programming

### 解题思路
需要好好考虑三角形的边界问题。比如 j== 0 和j==triangle(i).length-1。  
还有中间的部分需要用到dp。  
dp式式 r(i)(j) = scala.math.min(triangle(i-1)(j-1),triangle(i-1)(j))+triangle(i)(j)。  
然后在三角形的最后一行中找出最小值即可。
#### Scala
```scala
object Solution {
    def minimumTotal(triangle: List[List[Int]]): Int = {
        var len = triangle.length
        var r:List[List[Int]] = List()
        r = r :+ List(triangle(0)(0))
        for(i <- 1 until len){
            var temp:List[Int] = List()
            for(j <- 0 until triangle(i).length){
                if(j==0){
                    var t = r(i-1)(j) + triangle(i)(j)
                    temp = temp :+ t
                }else if(j==triangle(i).length-1){
                    var t = r(i-1)(j-1) + triangle(i)(j)
                    temp = temp :+ t
                }else{
                    var t = scala.math.min(r(i-1)(j-1),r(i-1)(j))+triangle(i)(j)
                    temp = temp :+ t
                }
            }
            r = r :+ temp
        }
        var res = r(len-1)(0)
        for(i <- 1 until r(len-1).length){
            res = scala.math.min(res,r(len-1)(i))
        }
        res
    }
}
```