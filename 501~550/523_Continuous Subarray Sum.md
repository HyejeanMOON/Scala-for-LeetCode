Given a list of non-negative numbers and a target integer k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of k, that is, sums up to n*k where n is also an integer.

Example 1:
```
Input: [23, 2, 4, 6, 7],  k=6
Output: True
Explanation: Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
```
Example 2:
```
Input: [23, 2, 6, 4, 7],  k=6
Output: True
Explanation: Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
```
Note:  
The length of the array won't exceed 10,000.
You may assume the sum of all the numbers is in the range of a signed 32-bit integer.

Difficulty:Medium  
Total Accepted:31.3K  
Total Submissions:134.2K  
Related Topics:Math, Dynamic Programming


### 解题思路
遍历搜索数组的所有子数组。如果子数组的和能整除k则返回true。当然作为特殊的例子是0的问题。
#### Scala
```scala
object Solution {
    def checkSubarraySum(nums: Array[Int], k: Int): Boolean = {
        var len = nums.length
        for(i <- 0 until len-1){
            var res = nums(i)
            for(j <- i+1 until len){
                res += nums(j)
                if(res == k) return true
                if(k!=0 && res % k ==0) return true
            }
        }
        false
    }
}
```
