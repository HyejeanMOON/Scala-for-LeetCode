Given four lists A, B, C, D of integer values, compute how many tuples (i, j, k, l) there are such that A[i] + B[j] + C[k] + D[l] is zero.

To make problem a bit easier, all A, B, C, D have same length of N where 0 ≤ N ≤ 500. All integers are in the range of -228 to 228 - 1 and the result is guaranteed to be at most 231 - 1.

Example:
```
Input:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

Output:
2

Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```

### 解题思路
如果用四个嵌套的for的话，时间复杂度是O(n4)。这样的话，时间复杂度过于大，所以两两循环。前一次的循环中用哈希表记录target以及出现的次数。第二次循环中，查找target，并相加结果。
#### Scala
```scala
object Solution {
    def fourSumCount(A: Array[Int], B: Array[Int], C: Array[Int], D: Array[Int]): Int = {
        var record:Map[Int,Int] = Map()
        var res = 0
        for(i <- 0 until A.length){
            for(j <- 0 until B.length){
                var sum = A(i) + B(j)
                var count = record.getOrElse(sum,0)
                count += 1
                record += (sum -> count)
            }
        }
        for(i <- 0 until C.length){
            for(j <- 0 until D.length){
                var target = 0 - C(i) -D(j)
                if(record.contains(target)){
                    res += record.getOrElse(target,0)
                }
            }
        }
        res
    }
}
```