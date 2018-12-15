Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example 1:
```
Input: [1,3,5,6], 5
Output: 2
```
Example 2:
```
Input: [1,3,5,6], 2
Output: 1
```
Example 3:
```
Input: [1,3,5,6], 7
Output: 4
```
Example 1:
```
Input: [1,3,5,6], 0
Output: 0
```

Difficulty:Easy  
Total Accepted:246.1K  
Total Submissions:615K  
Related Topics:Array, Binary Search


### 解题思路
使用二分法就很快能解决。
#### Scala
```scala
object Solution {
    def searchInsert(nums: Array[Int], target: Int): Int = {
        var len = nums.length
        var left = 0
        var right = len
        while(left<right){
            var mid = left + (right-left)/2
            if(nums(mid)>=target) right = mid
            else left = mid + 1      
        }
        right
    }
}
```