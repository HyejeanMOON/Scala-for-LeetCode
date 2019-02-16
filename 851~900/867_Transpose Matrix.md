Given a matrix A, return the transpose of A.

The transpose of a matrix is the matrix flipped over it's main diagonal, switching the row and column indices of the matrix.

 

Example 1:
```
Input: [[1,2,3],[4,5,6],[7,8,9]]
Output: [[1,4,7],[2,5,8],[3,6,9]]
Example 2:

Input: [[1,2,3],[4,5,6]]
Output: [[1,4],[2,5],[3,6]]
```

Note:

- 1 <= A.length <= 1000
- 1 <= A[0].length <= 1000


Difficulty:Easy  
Total Accepted:7K  
Total Submissions:10.3K  
Related Topics:Array

### 解题思路
#### Scala
```scala
object Solution {
    def transpose(A: Array[Array[Int]]): Array[Array[Int]] = {
        if(A.isEmpty) return A
        var res:Array[Array[Int]] = Array()     
        var col = A(0).length
        var row = A.length
        for(i <- 0 until col){
            var temp:Array[Int] = Array()
            for(j <- 0 until row){
                temp = temp :+ A(j)(i)
            }
            res = res :+ temp
            
        }
        res
    }
}
```