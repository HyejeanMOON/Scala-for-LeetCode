In MATLAB, there is a very useful function called 'reshape', which can reshape a matrix into a new one with different size but keep its original data.

You're given a matrix represented by a two-dimensional array, and two positive integers r and c representing the row number and column number of the wanted reshaped matrix, respectively.

The reshaped matrix need to be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the 'reshape' operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

Example 1:
```
Input: 
nums = 
[[1,2],
 [3,4]]
r = 1, c = 4
Output: 
[[1,2,3,4]]
Explanation:
The row-traversing of nums is [1,2,3,4]. The new reshaped matrix is a 1 * 4 matrix, fill it row by row by using the previous list.
```
Example 2:
```
Input: 
nums = 
[[1,2],
 [3,4]]
r = 2, c = 4
Output: 
[[1,2],
 [3,4]]
Explanation:
There is no way to reshape a 2 * 2 matrix to a 2 * 4 matrix. So output the original matrix.
```
Note:
The height and width of the given matrix is in range [1, 100].
The given r and c are all positive.

### 解题思路
1. 首先判断现有的长度是否可以满足要求，不满足就可以直接结束了。  
2. 把nums编程宽度为1的数组。方便进行重组。  
3. 然后对重组的数组进行遍历，再根据要求进行分割。


#### scala
```scala
object Solution {
    def matrixReshape(nums: Array[Array[Int]], r: Int, c: Int): Array[Array[Int]] = {
        var temp:Array[Int] = Array()
        var result:Array[Array[Int]] = Array()
        var row = nums.length
        var col = nums(0).length
        var flag = true
        for(i <- 0 until row){
            for(j <- 0 until col){
                temp = temp :+ nums(i)(j)
            }
        }
        if((r*c)!=(row*col)){
            flag = false
        }
        if(flag){
            var tempResult:Array[Int] = Array()
            var p = 0
                
                for(i <- 0 until r){
                    for(j <- 0 until c){
                        tempResult = tempResult :+ temp(p)
                        p += 1
                    }
                    result = result :+ tempResult
                    tempResult = Array()
                }
        }else{
            result = nums
        }
        result
    }
}
```