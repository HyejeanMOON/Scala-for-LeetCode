Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

Example 1:
```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```
Example 2:
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

Difficulty:Medium  
Total Accepted:254.4K  
Total Submissions:797.2K  
Related Topics:Array, Binary Search

### 解题思路



---


#### Scala
```scala
object Solution {
    def search(nums: Array[Int], target: Int): Int = {
        var head = 0
        while(head < nums.length){
            if(nums(head)==target) return head
            head += 1
        }
        -1
    }
}
```