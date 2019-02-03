Given a non-empty integer array, find the minimum number of moves required to make all array elements equal, where a move is incrementing a selected element by 1 or decrementing a selected element by 1.

You may assume the array's length is at most 10,000.

Example:
```
Input:
[1,2,3]

Output:
2

Explanation:
Only two moves are needed (remember each move increments or decrements one element):

[1,2,3]  =>  [2,2,3]  =>  [2,2,2]
```

Difficulty:Medium  
Total Accepted:26.5K  
Total Submissions:51.1K  
Related Topics:Math

### 解题思路
要求求最小数，所以只要以排序好的数组的中位数做为基准进行计算就可以了。
#### Scala
```scala
object Solution {
    def minMoves2(nums: Array[Int]): Int = {
        var n_sorted = nums.sorted
        var len = n_sorted.length
        var res = 0
        var mid = len/2
        for(n <- n_sorted){
            res+=scala.math.abs(n-n_sorted(mid))
        }
        res
    }
}
```