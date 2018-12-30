
Given a non-negative index k where k ≤ 33, return the kth index row of the Pascal's triangle.

Note that the row index starts from 0.


In Pascal's triangle, each number is the sum of the two numbers directly above it.

Example:
```
Input: 3
Output: [1,3,3,1]
```
Follow up:

Could you optimize your algorithm to use only O(k) extra space?

Difficulty:Easy  
Total Accepted:146.6K  
Total Submissions:381.3K  
Related Topics:Array

### 解题思路
#### Scala
```scala
object Solution {
    def getRow(rowIndex: Int): List[Int] = {
        var res:List[Int] = List()
        if(rowIndex==0) return List(1)
        if(rowIndex==1) return List(1,1)
        if(rowIndex>=2){
            var pre = List(1,1)
            for(i <- 2 to rowIndex){
                var temp:List[Int] = List()
                temp = temp :+ 1
                for(j <- 0 until pre.length-1){
                    var tt = pre(j) + pre(j+1)
                    temp = temp :+ tt
                }
                temp = temp :+ 1
                res = temp
                pre = temp
            }
        }
        res
    }
}
```