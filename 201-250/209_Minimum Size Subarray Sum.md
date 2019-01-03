Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.

Example: 
```
Input: [2,3,1,2,4,3], s = 7
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

Difficulty:Medium  
Total Accepted:117.6K  
Total Submissions:364.7K  
Related Topics:Array, Two Pointers, Binary Search

### 解题思路
用双循环，挨个查找。
#### Scala
```scala
object Solution {
    def minSubArrayLen(s: Int, nums: Array[Int]): Int = {
        var len = nums.length
        var min = len
        for(i <- 0 until len-1){
            var f = nums(i)
            var sum = f
            if(sum>=s) return 1
            var flag = true
            for(j <- i+1 until len if flag){
                sum += nums(j)
                if(sum>=s){
                    flag = false
                    if(min>(j-i+1)) min = j-i+1
                }
                
            }
            if(nums(len-1)>=s) return 1
        }
        if(nums.sum<s) min=0
        min
    }
}
```