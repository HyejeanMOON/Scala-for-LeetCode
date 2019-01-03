Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

Example 1:
```
Input: nums = [1,2,3,1], k = 3
Output: true
```
Example 2:
```
Input: nums = [1,0,1,1], k = 1
Output: true
```
Example 3:
```
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

Difficulty:Easy  
Total Accepted:150.4K  
Total Submissions:454.8K  
Related Topics:Array, Hash Table

### 解题思路
题的要求是两个重复的元素的坐标要小于等于k的情况返回true，否则返回false。
#### Scala
```scala
object Solution {
    def containsNearbyDuplicate(nums: Array[Int], k: Int): Boolean = {
        if(nums.length<=1) return false
        var record:Map[Int,Int] = Map()
        for(i <- 0 until nums.length){
            var temp = record.getOrElse(nums(i),-1)
            if(temp!=(-1)){
                if(i-temp <= k) return true
                else record+=(nums(i)->i)
            }else{
                record+=(nums(i)->i)
            }
        }
        false
    }
}
```