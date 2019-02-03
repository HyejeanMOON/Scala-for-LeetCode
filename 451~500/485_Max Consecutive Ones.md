Given a binary array, find the maximum number of consecutive 1s in this array.

Example 1:
```
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
```
Note:

The input array will only contain 0 and 1.
The length of input array is a positive integer and will not exceed 10,000

### 解题思路
遇到1就开始计数，然后碰到零就把计数结果记下来，把计数清零重新开始。

#### scala
```scala
object Solution {
    def findMaxConsecutiveOnes(nums: Array[Int]): Int = {
        var result:Int = 0
        var temp = 0
        for(i <- 0 until nums.length){
            if(nums(i) == 1){
                temp += 1
                if(temp > result){
                    result = temp
                }
            }else{
                temp = 0
            }
        }
        result  
    }
}
```