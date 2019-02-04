Given an m * n matrix M initialized with all 0's and several update operations.

Operations are represented by a 2D array, and each operation is represented by an array with two positive integers a and b, which means M[i][j] should be added by one for all 0 <= i < a and 0 <= j < b.

You need to count and return the number of maximum integers in the matrix after performing all the operations.

Example 1:
```
Input: 
m = 3, n = 3
operations = [[2,2],[3,3]]
Output: 4
Explanation: 
Initially, M = 
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]
 
After performing [2,2], M = 
[[1, 1, 0],
 [1, 1, 0],
 [0, 0, 0]]

After performing [3,3], M = 
[[2, 2, 1],
 [2, 2, 1],
 [1, 1, 1]]

So the maximum integer in M is 2, and there are four of it in M. So return 4.
```
Note:

The range of m and n is [1,40000].
The range of a is [1,m], and the range of b is [1,n].
The range of operations size won't exceed 10,000.

Difficulty:Easy  
Total Accepted:20.7K  
Total Submissions:43K  
Related Topics:Math

### 解题思路
寻找最小的范围，因为那个范围是一直被更新。返回横宽相乘数就可以了。
#### Scala
```scala
object Solution {
    def maxCount(m: Int, n: Int, ops: Array[Array[Int]]): Int = {
        var f = m
        var s = n
        for(op <- ops){
            f = scala.math.min(f,op(0))
            s = scala.math.min(s,op(1))
        }
        f*s
    }
}
```