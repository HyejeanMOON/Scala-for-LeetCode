Given a sorted (in ascending order) integer array nums of n elements and a target value, write a function to search target in nums. If target exists, then return its index, otherwise return -1.


Example 1:
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```
Example 2:
```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

Note:

You may assume that all elements in nums are unique.
n will be in the range [1, 10000].
The value of each element in nums will be in the range [-9999, 9999].

Difficulty:Easy  
Total Accepted:2.6K  
Total Submissions:14.5K  
Related Topics:Binary Search

### 解题思路
经典的二分法。
#### Scala
```Scala
object Solution {
    def search(nums: Array[Int], target: Int): Int = {
        if(nums.isEmpty) return -1
        var len = nums.length
        var left = 0
        var right = len-1
        if(len==1){
            if(nums(0)==target) return 0
            else return -1
        }
        
        while(left<right){
            var mid = (left+right)/2
            if(nums(left)==target) return left
            if(nums(right)==target) return right
            if(nums(mid)==target) return mid
            else if(nums(mid)<target){
                left=mid+1
            }else{
                right=mid-1
            }
            
        }
        
        -1
    }
}
```