Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

Note:  
1. Each of the array element will not exceed 100.
1. The array size will not exceed 200.

Example 1:
```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```
Example 2:
```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

### 解题思路





---

如果提供的数组内没有相同的数字的时候可以用这个方法，显然这个方法不太使用这道题。
#### Scala
```Scala
object Solution {
    def canPartition(nums: Array[Int]): Boolean = {
        if(nums.length==1) return false
        var sum = nums.sum
        var target = sum/2
        var dp = new scala.collection.mutable.ArrayBuffer[Int]()
        for(i <- 0 until sum){
            dp = dp :+ -1
        }
        for(i <- 0 until nums.length){
            var v = nums(i)
            if(dp(v)==(-1)) dp(v)=v
            else return true
        }
        false
    }
}
```