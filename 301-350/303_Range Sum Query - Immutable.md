Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

Example:
```
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```
Note:  
You may assume that the array does not change.
There are many calls to sumRange function.

Difficulty:Easy  
Total Accepted:99.4K  
Total Submissions:301.4K  
Related Topics:DP


### 解题思路
#### Scala
```scala
class NumArray(_nums: Array[Int]) {

    def sumRange(i: Int, j: Int): Int = {
        var sum = 0
        for(ii <- i to j){
            sum += _nums(ii)
        }
        sum
    }

}

/**
 * Your NumArray object will be instantiated and called as such:
 * var obj = new NumArray(nums)
 * var param_1 = obj.sumRange(i,j)
 */
```