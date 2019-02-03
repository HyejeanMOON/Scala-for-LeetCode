Given a non-empty integer array of size n, find the minimum number of moves required to make all array elements equal, where a move is incrementing n - 1 elements by 1.

Example:
```
Input:
[1,2,3]

Output:
3

Explanation:
Only three moves are needed (remember each move increments two elements):

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

### 解题思路
方法一：  
首先给数组排序，在循环中的使用最小值的原因是，怕溢出。结果是取和减去最小值乘于数组的长度。  
方法二：  
把n-1个元素加一进行换位思考。则是把一个元素减到跟最小值一样。这样会简单很多。

#### Scala
```
object Solution {
    def minMoves(nums: Array[Int]): Int = {
        var mv = scala.Int.MaxValue
        var num = nums.sorted
        var sum = 0
        for(i <- num){
            var temp = scala.math.min(i,mv)
            sum += temp
        }
        var res = sum - num(0)*num.length
        res
    }
}
```

```scala
//方法二
object Solution {
    def minMoves(nums: Array[Int]): Int = {
        var res = 0
        var mv = scala.Int.MaxValue
        var num = nums.sorted
        for(i <- 1 until num.length){
            res += num(i) - num(0)
        }
        res
    }
}
```