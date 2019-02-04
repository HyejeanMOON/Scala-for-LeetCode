Given an unsorted array of integers, find the length of longest continuous increasing subsequence (subarray).

Example 1:
```
Input: [1,3,5,4,7]
Output: 3
Explanation: The longest continuous increasing subsequence is [1,3,5], its length is 3. 
Even though [1,3,5,7] is also an increasing subsequence, it's not a continuous one where 5 and 7 are separated by 4. 
```
Example 2:
```
Input: [2,2,2,2,2]
Output: 1
Explanation: The longest continuous increasing subsequence is [2], its length is 1. 
```
Note: Length of the array will not exceed 10,000.

### 解题思路
比较当前的数字是否比前位大，如果是count加一，如果不是就判断是否是最大值。然后清空count。
#### Scala
```scala
object Solution {
    def findLengthOfLCIS(nums: Array[Int]): Int = {
        if(nums.length==0) return 0
        if(nums.length==1) return 1
        var res = 1
        var count = 1
        for(i <- 1 until nums.length){
            if(nums(i-1)<nums(i)){
                count += 1
            }else{
                if(res<count) res = count
                count =1
            }
        }
        if(res<count) res = count
        res
    }
}
```